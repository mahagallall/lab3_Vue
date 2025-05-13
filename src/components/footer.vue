<template>
  <footer class="bg-gradient text-white py-5 mt-5">
    <div class="container">
      <div class="row g-4 g-lg-5">
        
        <div class="col-lg-4 col-md-6 order-1 order-lg-0">
          <div class="mb-4">
            <h4 class="fw-bold mb-3 d-flex align-items-center">
              <i class="bi bi-mortarboard-fill text-primary me-2 fs-3"></i>Student Management
            </h4>
            <p class="text-light opacity-75 mb-4">
              Student Management System is a comprehensive platform designed to streamline the management of student data and academic records.
            </p>
            <div class="d-flex gap-3 social-icons">
              <a href="#" class="social-link" aria-label="Facebook"><i class="bi bi-facebook fs-5"></i></a>
              <a href="#" class="social-link" aria-label="Twitter"><i class="bi bi-twitter-x fs-5"></i></a>
              <a href="#" class="social-link" aria-label="Instagram"><i class="bi bi-instagram fs-5"></i></a>
              <a href="#" class="social-link" aria-label="LinkedIn"><i class="bi bi-linkedin fs-5"></i></a>
            </div>
          </div>
        </div>

        
        <div class="col-lg-2 col-md-6 order-2 order-lg-0">
          <h5 class="fw-bold mb-3 border-start border-primary border-4 ps-3">Navigation</h5>
          <ul class="list-unstyled footer-links">
            <li><a href="#" class="footer-link">Home</a></li>
            <li><a href="#" class="footer-link">Students</a></li>
            <li><a href="#" class="footer-link">Reports</a></li>
            <li><a href="#" class="footer-link">Settings</a></li>
          </ul>
        </div>

       
        <div class="col-lg-3 col-md-6 order-3 order-lg-0">
          <h5 class="fw-bold mb-3 border-start border-primary border-4 ps-3">Quick Links</h5>
          <ul class="list-unstyled footer-links">
            <li><a href="#" class="footer-link">Privacy Policy</a></li>
            <li><a href="#" class="footer-link">Terms of Service</a></li>
            <li><a href="#" class="footer-link">FAQ</a></li>
            <li><a href="#" class="footer-link">Support</a></li>
          </ul>
        </div>

        
        <div class="col-lg-3 col-md-6 order-4 order-lg-0">
          <h5 class="fw-bold mb-3 border-start border-primary border-4 ps-3">Contact Us</h5>
          <ul class="list-unstyled footer-contact">
            <li class="d-flex mb-3">
              <i class="bi bi-geo-alt-fill text-primary me-2 mt-1 fs-6"></i>
              <span class="text-light opacity-75">University Campus, Main Street, City, Country</span>
            </li>
            <li class="d-flex mb-3">
              <i class="bi bi-envelope-fill text-primary me-2 mt-1 fs-6"></i>
              <span class="text-light opacity-75">info@example.com</span>
            </li>
            <li class="d-flex mb-3">
              <i class="bi bi-telephone-fill text-primary me-2 mt-1 fs-6"></i>
              <span class="text-light opacity-75">(123) 456-7890</span>
            </li>
            <li class="d-flex">
              <i class="bi bi-clock-fill text-primary me-2 mt-1 fs-6"></i>
              <span class="text-light opacity-75">Mon-Fri: 9:00 AM - 5:00 PM</span>
            </li>
          </ul>
        </div>
      </div>

     
      <hr class="my-4 border-secondary">

      <div class="row align-items-center small">
        <div class="col-md-6 text-center text-md-start">
          <p class="mb-0">&copy; {{ new Date().getFullYear() }} Student Management System. All rights reserved.</p>
        </div>
        <div class="col-md-6 text-center text-md-end mt-3 mt-md-0">
          <div class="d-flex justify-content-center justify-content-md-end gap-3 flex-wrap">
            <a href="#" class="text-decoration-none text-muted">Privacy Policy</a>
            <span class="text-muted">|</span>
            <a href="#" class="text-decoration-none text-muted">Terms of Service</a>
            <span class="text-muted">|</span>
            <a href="#" class="text-decoration-none text-muted">Sitemap</a>
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
background-color: #474747;
 
  transition: background 0.3s ease;
}

.footer-links li {
  margin-bottom: 0.6rem;
}

.footer-link {
  color: rgba(127, 239, 237, 0.7);
  text-decoration: none;
  position: relative;
  display: inline-block;
  transition: all 0.3s ease;
}

.footer-link::after {
  content: '';
  position: absolute;
  width: 0%;
  height: 1px;
  bottom: -2px;
  left: 0;
  background-color: #94eaa5;
  transition: 0.3s ease;
}

.footer-link:hover::after {
  width: 100%;
}

.social-icons .social-link {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  color: #69dfdb;
  transition: all 0.3s ease;
}

.social-icons .social-link:hover {
  background-color: #8986e9;
  color: #053f14;
  transform: translateY(-3px);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.footer-contact i {
  font-size: 1.1rem;
}

hr {
  opacity: 0.2;
}

@media (max-width: 767.98px) {
  .footer-links,
  .footer-contact {
    margin-bottom: 1.5rem;
  }

  .social-icons {
    justify-content: start;
  }
}
</style>