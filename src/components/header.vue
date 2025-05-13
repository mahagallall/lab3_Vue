<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-gradient shadow-sm" style="background-color: #474747;">
    <div class="container-fluid">
      <a class="navbar-brand d-flex align-items-center" href="#">
        <i class="bi bi-mortarboard-fill me-2 fs-4 text-primary"></i>
        <span class="fw-bold" style="color: aqua;">Student Dashboard</span>
      </a>

      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active fw-medium" aria-current="page" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link fw-medium" href="#">Students</a>
          </li>
          <li class="nav-item">
            <a class="nav-link fw-medium" href="#">Reports</a>
          </li>
          <li class="nav-item">
            <a class="nav-link fw-medium" href="#">Settings</a>
          </li>
        </ul>

        <form class="d-flex position-relative w-100 w-lg-auto">
          <input class="form-control rounded-pill ps-4 search-input" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-primary rounded-circle position-absolute top-50 end-0 translate-middle-y me-1"
            type="submit">
            <i class="bi bi-search"></i>
          </button>
        </form>

        <div class="d-flex ms-3 align-items-center mt-3 mt-lg-0">
          <button class="btn btn-outline-light rounded-circle mx-2" title="Notifications">
            <i class="bi bi-bell fs-5"></i>
          </button>
          <button class="btn btn-outline-light rounded-circle mx-2" title="Profile">
            <i class="bi bi-person-circle fs-5"></i>
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "HeaderComponent"
}
</script>

<style scoped>

.bg-gradient {
  background: linear-gradient(90deg, #54e7f2, #1a1a1a);
}

.navbar-brand {
  font-size: 1.3rem;
  transition: transform 0.2s ease;
}

.navbar-brand:hover {
  transform: scale(1.05);
}

.nav-link {
  color: rgba(52, 227, 227, 0.85) !important;
  padding: 0.5rem 0.8rem !important;
  margin: 0 0.3rem;
  transition: all 0.3s ease;
}

.nav-link.active,
.nav-link:hover {
  color: #eb46d2 !important;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 0.375rem;
}

.search-input {
  padding-right: 2.5rem;
  transition: all 0.3s ease;
}

.search-input:focus {
  box-shadow: 0 0 8px rgba(13, 110, 253, 0.4);
  outline: none;
}

.btn-primary {
  background-color: #2bcbe8;
  border: none;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-primary:hover {
  background-color: #f043f3;
}

@media (max-width: 767.98px) {
  .search-input {
    width: 100%;
    margin-bottom: 0.75rem;
  }

  .ms-3 {
    margin-left: 0 !important;
  }
}
</style>