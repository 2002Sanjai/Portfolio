<script setup>
import { User } from 'lucide-vue-next'
</script>

<template>
  <section id="about" class="section about">
    <div class="about-header">
      <div class="icon-circle">
        <User :size="32" class="icon-accent" />
      </div>
      <h2 class="section-title">About Me</h2>
    </div>
    
    <div class="about-container glass-panel">
      <div class="about-content">
        <p>
          I am a passionate <strong>Frontend Developer</strong> with 2 years of professional experience specializing in scalable, responsive, and user-friendly applications. I hold a <strong>Bachelor of Engineering</strong> with an 8.05 CGPA from Prince Shri Venkateshwara Padmavathy Engineering College.
        </p>
        <p>
          My expertise lies in modern front-end frameworks like <strong>Vue.js</strong> and <strong>React.js</strong>, along with backend technologies such as <strong>Node.js</strong> and RESTful APIs. I am proficient with tools like GitHub Actions, Jira, and various testing libraries, and have an unwavering commitment to writing clean, maintainable, and high-performance code.
        </p>
        <p>
          Beyond technical work, I thrive in collaborative environments, continuously seeking to learn, mentor, and share knowledge to drive innovation across teams.
        </p>
      </div>
    </div>
  </section>
</template>


<style scoped>
.about-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.icon-circle {
  width: 60px;
  height: 60px;
  background: rgba(67, 97, 238, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(67, 97, 238, 0.2);
}

.icon-accent {
  color: var(--accent-primary);
}

.about-container {
  padding: 1.5rem 2rem;
  max-width: 900px;
  margin: 0 auto;
}


.about-content {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.about-content p {
  color: var(--text-secondary);
  font-size: 1.1rem;
  line-height: 1.8;
}

strong {
  color: var(--text-primary);
  font-weight: 600;
}

@media (max-width: 768px) {
  .about-container {
    padding: 2rem;
  }
}
</style>
