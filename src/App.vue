<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Education from './components/Education.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
</script>

<template>
  <div class="portfolio-wrapper">
    <Navbar />
    <main>
      <Hero />
      <div class="container">
        <About />
        <Skills />
        <Experience />
        <Education />
        <Projects />
      </div>
    </main>
    <Contact />
  </div>
</template>

<style scoped>
.portfolio-wrapper {
  position: relative;
  min-height: 100vh;
}

/* Background blob effects for premium aesthetic */
.portfolio-wrapper::before,
.portfolio-wrapper::after {
  content: '';
  position: fixed;
  border-radius: 50%;
  filter: blur(100px);
  z-index: -1;
  opacity: 0.15;
}

.portfolio-wrapper::before {
  top: -10%;
  left: -10%;
  width: 50vw;
  height: 50vw;
  background: var(--accent-primary);
}

.portfolio-wrapper::after {
  bottom: -10%;
  right: -10%;
  width: 40vw;
  height: 40vw;
  background: var(--accent-secondary);
}
</style>
