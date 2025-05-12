<template>
  <footer class="bg-dark text-white py-5 mt-5">
    <div class="container">
      <div class="row g-4">
        <div class="col-lg-4 col-md-6">
          <div class="mb-4">
            <h4 class="fw-bold mb-3">
              <i class="bi bi-mortarboard-fill text-primary me-2"></i>Student Management
            </h4>
            <p class="text-muted mb-3">
              A simple yet powerful system to manage student records and information efficiently and securely.
            </p>
            <div class="d-flex gap-3 social-icons">
              <a href="#" class="text-white"><i class="bi bi-facebook fs-4"></i></a>
              <a href="#" class="text-white"><i class="bi bi-twitter-x fs-4"></i></a>
              <a href="#" class="text-white"><i class="bi bi-instagram fs-4"></i></a>
              <a href="#" class="text-white"><i class="bi bi-linkedin fs-4"></i></a>
            </div>
          </div>
        </div>
        
        <div class="col-lg-2 col-md-6">
          <h5 class="fw-bold mb-3 border-start border-primary border-4 ps-3">Navigation</h5>
          <ul class="list-unstyled footer-links">
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Home
              </a>
            </li>
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Students
              </a>
            </li>
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Reports
              </a>
            </li>
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Settings
              </a>
            </li>
          </ul>
        </div>
        
        <div class="col-lg-3 col-md-6">
          <h5 class="fw-bold mb-3 border-start border-primary border-4 ps-3">Quick Links</h5>
          <ul class="list-unstyled footer-links">
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Privacy Policy
              </a>
            </li>
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Terms of Service
              </a>
            </li>
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>FAQ
              </a>
            </li>
            <li class="mb-2">
              <a href="#" class="text-decoration-none text-muted">
                <i class="bi bi-chevron-right me-1 small"></i>Support
              </a>
            </li>
          </ul>
        </div>
        
        <div class="col-lg-3 col-md-6">
          <h5 class="fw-bold mb-3 border-start border-primary border-4 ps-3">Contact Us</h5>
          <ul class="list-unstyled footer-contact">
            <li class="d-flex mb-3">
              <i class="bi bi-geo-alt-fill text-primary me-2 mt-1"></i>
              <span class="text-muted">University Campus, Main Street, City, Country</span>
            </li>
            <li class="d-flex mb-3">
              <i class="bi bi-envelope-fill text-primary me-2 mt-1"></i>
              <span class="text-muted">info@example.com</span>
            </li>
            <li class="d-flex mb-3">
              <i class="bi bi-telephone-fill text-primary me-2 mt-1"></i>
              <span class="text-muted">(123) 456-7890</span>
            </li>
            <li class="d-flex">
              <i class="bi bi-clock-fill text-primary me-2 mt-1"></i>
              <span class="text-muted">Mon-Fri: 9:00 AM - 5:00 PM</span>
            </li>
          </ul>
        </div>
      </div>
      
      <hr class="my-4 border-secondary">
      
      <div class="row align-items-center">
        <div class="col-md-6 text-center text-md-start">
          <p class="mb-0">&copy; {{ new Date().getFullYear() }} Student Management System. All rights reserved.</p>
        </div>
        <div class="col-md-6 text-center text-md-end mt-3 mt-md-0">
          <div class="d-flex justify-content-center justify-content-md-end gap-3">
            <a href="#" class="text-decoration-none text-muted small">Privacy Policy</a>
            <span class="text-muted">|</span>
            <a href="#" class="text-decoration-none text-muted small">Terms of Service</a>
            <span class="text-muted">|</span>
            <a href="#" class="text-decoration-none text-muted small">Sitemap</a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "FooterComponent"
}
</script>

<style scoped>
footer {
  box-shadow: 0 -5px 15px rgba(0,0,0,0.1);
}

.footer-links a, .social-icons a {
  transition: all 0.3s ease;
  display: inline-block;
}

.footer-links a:hover {
  color: #0d6efd !important;
  transform: translateX(5px);
}

.social-icons a {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background-color: rgba(255,255,255,0.1);
  display: flex;
  justify-content: center;
  align-items: center;
}

.social-icons a:hover {
  background-color: #0d6efd;
  transform: translateY(-3px);
}

.footer-contact li {
  margin-bottom: 10px;
}

.footer-contact i {
  font-size: 1.1rem;
}

hr {
  opacity: 0.2;
}

@media (max-width: 767.98px) {
  .footer-links, .footer-contact {
    margin-bottom: 2rem;
  }
}
</style>