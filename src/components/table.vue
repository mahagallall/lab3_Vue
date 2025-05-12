<template>
  <div>
    <div v-if="loading" class="text-center my-5">
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
      <p class="mt-2">Loading students data...</p>
    </div>
    
    <div v-else-if="error" class="alert alert-danger">
      {{ errorMessage }}
    </div>
    
    <div v-else>
      <div class="d-flex justify-content-between align-items-center mb-3">
        <h4 class="mb-0">Student Records</h4>
        <div class="input-group" style="max-width: 300px;">
          <input 
            type="text" 
            class="form-control" 
            placeholder="Search students..." 
            v-model="searchQuery"
            @input="performSearch"
          >
          <button class="btn btn-outline-secondary" type="button" @click="clearSearch" v-if="searchQuery">
            <i class="bi bi-x-lg"></i>
          </button>
          <button class="btn btn-outline-primary" type="button">
            <i class="bi bi-search"></i>
          </button>
        </div>
      </div>
      
      <div class="card mb-3" v-if="searchQuery">
        <div class="card-body bg-light py-2">
          <div class="d-flex align-items-center">
            <span class="me-2"><i class="bi bi-funnel-fill text-primary"></i></span>
            <span>Filtering by: <strong>"{{ searchQuery }}"</strong></span>
            <button class="btn btn-sm btn-link ms-auto" @click="clearSearch">Clear Filter</button>
          </div>
        </div>
      </div>
      
      <div class="table-responsive">
        <table class="table table-hover">
          <thead class="table-light">
            <tr>
              <th scope="col" class="text-center">#</th>
              <th scope="col">
                <div class="d-flex align-items-center">
                  Name
                  <button class="btn btn-sm ms-2" @click="sortBy('name')">
                    <i class="bi" :class="getSortIcon('name')"></i>
                  </button>
                </div>
              </th>
              <th scope="col">
                <div class="d-flex align-items-center">
                  City
                  <button class="btn btn-sm ms-2" @click="sortBy('city')">
                    <i class="bi" :class="getSortIcon('city')"></i>
                  </button>
                </div>
              </th>
              <th scope="col" class="text-center">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-if="filteredStudents.length === 0">
              <td colspan="4" class="text-center py-4">
                <div class="alert alert-info mb-0">
                  <i class="bi bi-exclamation-circle me-2"></i>
                  No students found. Try a different search or add a new student.
                </div>
              </td>
            </tr>
            <tr v-for="student in paginatedStudents" :key="student.id" class="align-middle">
              <td class="text-center">{{student.id}}</td>
              <td>{{student.name}}</td>
              <td>{{ student.city }}</td>
              <td class="text-center">
                <button class="btn btn-sm btn-outline-primary me-1" title="Edit">
                  <i class="bi bi-pencil"></i>
                </button>
                <button class="btn btn-sm btn-outline-danger" title="Delete" @click="confirmDelete(student)">
                  <i class="bi bi-trash"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      
      <div class="d-flex justify-content-between align-items-center mt-3">
        <p class="text-muted mb-0">
          Showing {{ paginatedStudents.length }} of {{ filteredStudents.length }} students
          <span v-if="searchQuery"> (filtered from {{ students.length }} total)</span>
        </p>
        <nav aria-label="Page navigation" v-if="totalPages > 1">
          <ul class="pagination pagination-sm mb-0">
            <li class="page-item" :class="{ disabled: currentPage === 1 }">
              <a class="page-link" href="#" @click.prevent="changePage(currentPage - 1)">Previous</a>
            </li>
            <li 
              v-for="page in displayedPages" 
              :key="page" 
              class="page-item"
              :class="{ active: page === currentPage }"
            >
              <a class="page-link" href="#" @click.prevent="changePage(page)">{{ page }}</a>
            </li>
            <li class="page-item" :class="{ disabled: currentPage === totalPages }">
              <a class="page-link" href="#" @click.prevent="changePage(currentPage + 1)">Next</a>
            </li>
          </ul>
        </nav>
      </div>

      <!-- Delete Confirmation Modal -->
      <div class="modal fade" id="deleteModal" tabindex="-1" aria-labelledby="deleteModalLabel" aria-hidden="true" ref="deleteModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header bg-danger text-white">
              <h5 class="modal-title" id="deleteModalLabel">Confirm Delete</h5>
              <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body" v-if="studentToDelete">
              <p>Are you sure you want to delete student <strong>{{ studentToDelete.name }}</strong>?</p>
              <p class="mb-0 text-danger"><small>This action cannot be undone.</small></p>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
              <button type="button" class="btn btn-danger" @click="deleteStudent" :disabled="isDeleting">
                <span v-if="isDeleting" class="spinner-border spinner-border-sm me-1" role="status"></span>
                Delete
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    students: [],
    loading: true,
    error: false,
    errorMessage: '',
    searchQuery: '',
    currentPage: 1,
    pageSize: 5,
    studentToDelete: null,
    isDeleting: false,
    sortField: null,
    sortDirection: 'asc'
  }),
  computed: {
    filteredStudents() {
      if (!this.searchQuery) return this.sortedStudents;
      
      const query = this.searchQuery.toLowerCase().trim();
      return this.sortedStudents.filter(student => 
        student.name.toLowerCase().includes(query) || 
        student.city.toLowerCase().includes(query) ||
        String(student.id).includes(query)
      );
    },
    sortedStudents() {
      if (!this.sortField) return this.students;
      
      return [...this.students].sort((a, b) => {
        let fieldA = a[this.sortField].toLowerCase();
        let fieldB = b[this.sortField].toLowerCase();
        
        if (this.sortDirection === 'asc') {
          return fieldA > fieldB ? 1 : -1;
        } else {
          return fieldA < fieldB ? 1 : -1;
        }
      });
    },
    totalPages() {
      return Math.ceil(this.filteredStudents.length / this.pageSize);
    },
    paginatedStudents() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.filteredStudents.slice(start, end);
    },
    displayedPages() {
      // Show at most 5 page numbers
      const pages = [];
      const totalPages = this.totalPages;
      
      if (totalPages <= 5) {
        // Show all pages if there are 5 or fewer
        for (let i = 1; i <= totalPages; i++) {
          pages.push(i);
        }
      } else {
        // Always show current page, 2 before and 2 after if possible
        const startPage = Math.max(1, this.currentPage - 2);
        const endPage = Math.min(totalPages, startPage + 4);
        
        for (let i = startPage; i <= endPage; i++) {
          pages.push(i);
        }
      }
      
      return pages;
    }
  },
  methods: {
    performSearch() {
      // Reset to first page when searching
      this.currentPage = 1;
    },
    clearSearch() {
      this.searchQuery = '';
      this.currentPage = 1;
    },
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    confirmDelete(student) {
      this.studentToDelete = student;
      // Show the modal using Bootstrap's JS API
      const modal = new bootstrap.Modal(document.getElementById('deleteModal'));
      modal.show();
    },
    async deleteStudent() {
      if (!this.studentToDelete) return;
      
      this.isDeleting = true;
      
      try {
        const response = await fetch(`http://localhost:3001/students/${this.studentToDelete.id}`, {
          method: 'DELETE'
        });
        
        if (!response.ok) {
          throw new Error(`Server responded with status: ${response.status}`);
        }
        
        // Remove from local array
        this.students = this.students.filter(s => s.id !== this.studentToDelete.id);
        
        // Close modal
        const modal = bootstrap.Modal.getInstance(document.getElementById('deleteModal'));
        modal.hide();
        
        // Reset
        this.studentToDelete = null;
        
        // If current page is now empty, go to previous page
        if (this.paginatedStudents.length === 0 && this.currentPage > 1) {
          this.currentPage--;
        }
      } catch (err) {
        console.error("Error deleting student:", err);
        alert("Failed to delete student. Please try again.");
      } finally {
        this.isDeleting = false;
      }
    },
    sortBy(field) {
      // If clicking on the same field, toggle direction
      if (this.sortField === field) {
        this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
      } else {
        // New field, set to ascending
        this.sortField = field;
        this.sortDirection = 'asc';
      }
    },
    getSortIcon(field) {
      if (this.sortField !== field) {
        return 'bi-arrow-down-up text-muted';
      }
      return this.sortDirection === 'asc' 
        ? 'bi-sort-alpha-down text-primary' 
        : 'bi-sort-alpha-up text-primary';
    }
  },
  async mounted() {
    try {
      this.loading = true;
      let response = await fetch("http://localhost:3001/students");
      
      if (!response.ok) {
        throw new Error(`Server responded with status: ${response.status}`);
      }
      
      this.students = await response.json();
      this.loading = false;
    } catch (err) {
      this.error = true;
      this.errorMessage = "Failed to fetch students data. Please make sure the API server is running at http://localhost:3001";
      console.error("Error fetching students:", err);
      this.loading = false;
    }
  }
}
</script>

<style scoped>
.table th {
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.85rem;
  letter-spacing: 0.5px;
}

.table td {
  vertical-align: middle;
}

.table-hover tbody tr:hover {
  background-color: rgba(13, 110, 253, 0.05);
}

.btn-outline-primary, .btn-outline-danger {
  padding: 0.25rem 0.5rem;
}

.pagination .page-link {
  color: #0d6efd;
  border-color: #dee2e6;
}

.pagination .page-item.active .page-link {
  background-color: #0d6efd;
  border-color: #0d6efd;
}

.btn-outline-secondary:hover {
  background-color: #f8f9fa;
  color: #6c757d;
  border-color: #6c757d;
}

.card-body.bg-light {
  background-color: #f8f9fa !important;
}

.btn-sm.btn-link {
  text-decoration: none;
  padding: 0.25rem 0.5rem;
}

.btn-sm.btn-link:hover {
  text-decoration: underline;
}

button.btn.btn-sm {
  padding: 0.1rem 0.3rem;
}
</style>