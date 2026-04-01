<script setup>
import { Mail, Phone, MessageSquare } from 'lucide-vue-next'
</script>

<template>
  <footer id="contact" class="contact-section">
    <div class="container text-center">
      <div class="contact-header">
        <MessageSquare class="title-icon" :size="40" />
        <h2 class="title">Let's Connect</h2>
      </div>
      <p class="subtitle">Looking for an experienced Frontend Developer for your next project?</p>
      
      <div class="contact-methods">
        <a href="mailto:sanjai25082002@gmail.com" class="contact-pill glass-panel">
          <Mail :size="20" class="pill-icon" />
          sanjai25082002@gmail.com
        </a>
        <a href="tel:+919789626910" class="contact-pill glass-panel">
          <Phone :size="20" class="pill-icon" />
          +91 9789626910
        </a>
      </div>


      <div class="footer-bottom">
        <p>&copy; {{ new Date().getFullYear() }} Sanjai M. All Rights Reserved.</p>
        <p class="built-with">Built with Vue.js & Vanilla CSS</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.contact-section {
  padding: 8rem 0 4rem;
  background: linear-gradient(to top, rgba(67, 97, 238, 0.05), transparent);
  border-top: 1px solid var(--border-light);
  margin-top: 5rem;
}

.text-center {
  text-align: center;
}

.title {
  font-size: 3rem;
  font-weight: 800;
  color: var(--text-primary);
}

.contact-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.title-icon {
  color: var(--accent-primary);
  filter: drop-shadow(0 0 10px rgba(67, 97, 238, 0.4));
  animation: float 4s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.subtitle {
  font-size: 1.2rem;
  color: var(--text-secondary);
  max-width: 600px;
  margin: 0 auto 3rem;
}

.contact-methods {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
  margin-bottom: 5rem;
}

.contact-pill {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  padding: 1.2rem 2.5rem;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--text-primary);
  transition: var(--transition-smooth);
}

.contact-pill:hover {
  transform: translateY(-8px);
  background: var(--accent-gradient);
  border-color: transparent;
  box-shadow: 0 15px 30px rgba(67, 97, 238, 0.4);
  color: #fff;
}

.pill-icon {
  color: var(--accent-primary);
  transition: var(--transition-smooth);
}

.contact-pill:hover .pill-icon {
  color: #fff;
  transform: scale(1.2);
}


.footer-bottom {
  padding-top: 3rem;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-bottom p {
  color: var(--text-secondary);
  font-size: 0.95rem;
}

.built-with {
  font-weight: 600;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

@media (max-width: 768px) {
  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }
}
</style>
