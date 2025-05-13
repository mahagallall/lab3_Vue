<template>
  <div>
    <button type="button" class="btn btn-primary mb-4" data-bs-toggle="modal" data-bs-target="#studentModal">
      <i class="bi bi-plus-circle me-2"></i>Add Student
    </button>

    <div class="modal fade" id="studentModal" tabindex="-1" aria-labelledby="studentModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header bg-primary text-white">
            <h5 class="modal-title" id="studentModalLabel">Add New Student</h5>
            <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form>
              <div class="mb-3">
                <label for="name" class="form-label">Student Name</label>
                <input 
                  type="text" 
                  class="form-control" 
                  id="name" 
                  v-model="name"
                  placeholder="Enter full name"
                  :class="{'is-invalid': nameError}"
                >
                <div v-if="nameError" class="invalid-feedback">
                  Please enter a valid name
                </div>
              </div>
              <div class="mb-3">
                <label for="city" class="form-label">City</label>
                <input 
                  class="form-control" 
                  id="city" 
                  v-model="city"
                  placeholder="Enter city"
                  :class="{'is-invalid': cityError}"
                />
                <div v-if="cityError" class="invalid-feedback">
                  Please enter a valid city
                </div>
              </div>
            </form>
            <div v-if="submitError" class="alert alert-danger mt-3">
              {{ errorMessage }}
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
              <i class="bi bi-x-circle me-1"></i>Cancel
            </button>
            <button 
              type="button" 
              class="btn btn-primary" 
              @click="addStudent"
              :disabled="isSubmitting"
            >
              <span v-if="isSubmitting" class="spinner-border spinner-border-sm me-1" role="status"></span>
              <i v-else class="bi bi-check-circle me-1"></i>Save Student
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    name: '',
    city: '',
    nameError: false,
    cityError: false,
    submitError: false,
    errorMessage: '',
    isSubmitting: false
  }),
  methods: {
    validateForm() {
      this.nameError = !this.name.trim();
      this.cityError = !this.city.trim();
      return !this.nameError && !this.cityError;
    },
    async addStudent() {
      if (!this.validateForm()) return;
      
      this.isSubmitting = true;
      this.submitError = false;
      
      const data = {
        name: this.name.trim(),
        city: this.city.trim()
      };
      
      try {
        const response = await fetch("http://localhost:3001/students", {
          method: "POST",
          body: JSON.stringify(data),
          headers: {"Content-Type": "application/json"}
        });
        
        if (!response.ok) {
          throw new Error(`Server responded with status: ${response.status}`);
        }
        
        
        this.name = '';
        this.city = '';
        this.nameError = false;
        this.cityError = false;
        
        
        document.querySelector('[data-bs-dismiss="modal"]').click();
        
        
        this.$emit('student-added');
        
        
        this.showAlert('Student added successfully!', 'success');
      } catch (err) {
        console.error("Error adding student:", err);
        this.submitError = true;
        this.errorMessage = "Failed to add student. Please make sure the API server is running.";
      } finally {
        this.isSubmitting = false;
      }
    },
    showAlert(message, type = 'info') {
      
      
      alert(message);
    }
  }
};
</script>

<style scoped>
.modal-header {
  border-bottom: 0;
}

.modal-footer {
  border-top: 0;
}

.btn-primary, .btn-secondary {
  padding: 0.5rem 1.5rem;
}

.form-label {
  font-weight: 500;
}

.form-control:focus {
  border-color: #28e3e0;
  box-shadow: 0 0 0 0.25rem rgba(14, 225, 215, 0.25);
}
</style>
