<script setup>
import RadiumHero from './RadiumHero.vue'
</script>
 
<template>
  <section class="hero section">
    <div class="container hero-content animate-fade-in">
      <div class="hero-text">
        <p class="greeting">Hi there, I'm</p>
        <h1 class="name">Sanjai M</h1>
        <h2 class="role">Frontend Developer</h2>
        <p class="bio">
          I build scalable, responsive, and user-friendly web applications.
          Passionate about clean code, modern frameworks, and seamless user experiences.
        </p>
        <div class="cta-group">
          <a href="#projects" class="btn btn-primary">View My Work</a>
          <a href="#contact" class="btn btn-secondary">Get In Touch</a>
        </div>
      </div>
      <div class="hero-visual">
        <RadiumHero />
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 70vh;
  display: flex;
  align-items: center;
  padding-top: 100px;
}

.hero-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 3rem;
}

.hero-text {
  max-width: 600px;
  flex: 1;
}

.hero-visual {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 350px;
}

.greeting {
  font-size: 1.25rem;
  color: var(--accent-secondary);
  font-weight: 500;
  margin-bottom: 0.5rem;
  letter-spacing: 1px;
}

.name {
  font-size: clamp(3rem, 8vw, 5rem);
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 0.5rem;
  color: var(--text-primary);
}

.role {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  font-weight: 600;
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
}

.bio {
  font-size: 1.15rem;
  color: var(--text-secondary);
  line-height: 1.8;
  max-width: 600px;
  margin-bottom: 2.5rem;
}

.cta-group {
  display: flex;
  gap: 1rem;
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.8rem 2rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  transition: var(--transition-smooth);
  cursor: pointer;
  border: none;
}

.btn-primary {
  background: var(--accent-gradient);
  color: white;
  box-shadow: 0 4px 15px rgba(67, 97, 238, 0.3);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(67, 97, 238, 0.4);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-primary);
  border: 1px solid var(--border-light);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .hero-content {
    flex-direction: column-reverse;
    justify-content: center;
    text-align: center;
    gap: 2rem;
  }
  
  .hero-text {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .cta-group {
    flex-direction: column;
    width: 100%;
    max-width: 300px;
  }
}
</style>
