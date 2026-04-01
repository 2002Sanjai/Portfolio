<script setup>
import { ref, onMounted } from 'vue'
import { 
  User, Code, Briefcase, GraduationCap, Folder, Mail, Sun, Moon 
} from 'lucide-vue-next'

const isDark = ref(true)

const toggleTheme = () => {
  isDark.value = !isDark.value
  document.documentElement.setAttribute('data-theme', isDark.value ? 'dark' : 'light')
}

onMounted(() => {
  // Initialize dark mode as default or use local storage/system pref
  const storedTheme = localStorage.getItem('theme')
  if (storedTheme === 'light') {
    isDark.value = false
    document.documentElement.setAttribute('data-theme', 'light')
  }
})

// Optional: watch to save preference
import { watch } from 'vue'
watch(isDark, (newVal) => {
  localStorage.setItem('theme', newVal ? 'dark' : 'light')
})
</script>

<template>
  <nav class="navbar glass-panel">
    <div class="nav-brand">
      <span class="logo">Sanjai<span class="highlight">.</span>M</span>
    </div>
    <ul class="nav-links">
      <li>
        <a href="#about">
          <User class="nav-icon" :size="18" />
          About
        </a>
      </li>
      <li>
        <a href="#skills">
          <Code class="nav-icon" :size="18" />
          Skills
        </a>
      </li>
      <li>
        <a href="#experience">
          <Briefcase class="nav-icon" :size="18" />
          Experience
        </a>
      </li>
      <li>
        <a href="#education">
          <GraduationCap class="nav-icon" :size="18" />
          Education
        </a>
      </li>
      <li>
        <a href="#projects">
          <Folder class="nav-icon" :size="18" />
          Projects
        </a>
      </li>
      <li>
        <a href="#contact" class="btn btn-outline">
          <Mail class="nav-icon" :size="18" />
          Contact Me
        </a>
      </li>
      <li>
        <button class="theme-toggle" @click="toggleTheme" aria-label="Toggle dark mode">
          <Sun v-if="isDark" :size="20" color="#ffb703" />
          <Moon v-else :size="20" color="#4cc9f0" />
        </button>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  max-width: 1200px;
  z-index: 1000;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  border-radius: 50px;
}

.logo {
  font-size: 1.5rem;
  font-weight: 800;
  letter-spacing: -0.5px;
}

.highlight {
  color: var(--accent-primary);
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.nav-links a {
  font-size: 0.95rem;
  font-weight: 500;
  transition: var(--transition-smooth);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.nav-links a:hover {
  color: var(--accent-secondary);
}

.nav-icon {
  opacity: 0.8;
  transition: var(--transition-smooth);
}

.nav-links a:hover .nav-icon {
  transform: translateY(-2px);
  opacity: 1;
}

.btn-outline {
  padding: 0.5rem 1.2rem;
  border: 1px solid var(--accent-primary);
  border-radius: 30px;
  color: var(--accent-primary) !important;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}


.btn-outline:hover {
  background: var(--accent-primary);
  color: #fff !important;
}

.theme-toggle {
  background: none;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 50%;
  transition: var(--transition-smooth);
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
}

.theme-toggle:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: rotate(15deg);
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
}
</style>
