<script setup>
import { ref, markRaw } from 'vue'
import { 
  Folder, Code2, ExternalLink, 
  Layout, Atom, Server, Database, Layers, Box, Terminal, Cpu, Zap
} from 'lucide-vue-next'

const getTechIcon = (tech) => {
  const name = tech.toLowerCase()
  if (name.includes('vue')) return markRaw(Layout)
  if (name.includes('react')) return markRaw(Atom)
  if (name.includes('node')) return markRaw(Server)
  if (name.includes('mongo') || name.includes('sql') || name.includes('db')) return markRaw(Database)
  if (name.includes('typescript') || name.includes('js')) return markRaw(Code2)
  if (name.includes('pinia') || name.includes('vuex')) return markRaw(Layers)
  if (name.includes('bootstrap') || name.includes('vuetify') || name.includes('ant')) return markRaw(Box)
  return markRaw(Terminal)
}

const projects = ref([
  {
    title: 'AI-Driven Conversation Analytics',
    role: 'Frontend Developer',
    tech: ['Vue.js', 'TypeScript', 'Pinia', 'Ant Design', 'Node.js', 'MongoDB', 'Ag Grid'],
    description: 'Developed a comprehensive AI-powered conversational analytics platform integrating transcription, translation, and real-time data visualization. Handled multilingual content seamlessly while implementing advanced search, filtering, and stats using Ag Grid.'
  },
  {
    title: 'Traveloplex',
    role: 'Frontend Developer',
    tech: ['Vue.js', 'Vuex', 'Bootstrap', 'Vuetify'],
    description: 'A modern flight booking system built with Vue.js. Integrates advanced API services for real-time flight availability, payment gateway handling, and efficient state management using Vuex for seamless user experience.'
  }
])
</script>


<template>
  <section id="projects" class="section projects">
    <div class="header-compact">
      <Zap class="header-icon" :size="24" />
      <h2 class="section-title compact">Featured Projects</h2>
    </div>
    
    <div class="projects-grid">
      <div v-for="(project, index) in projects" :key="index" class="project-card glass-panel">
        <div class="card-content">
          <div class="project-header">
            <div class="title-area">
              <Folder class="folder-icon" :size="18" />
              <h3 class="project-title">{{ project.title }}</h3>
            </div>
            <ExternalLink class="link-icon" :size="14" />
          </div>
          
          <div class="project-role-badge">
            <Code2 :size="12" />
            {{ project.role }}
          </div>
          
          <p class="project-desc">{{ project.description }}</p>

          <div class="tech-stack">
            <span v-for="(tech, tIndex) in project.tech" :key="tIndex" class="tech-badge">
              <component :is="getTechIcon(tech)" :size="12" class="badge-icon" />
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects {
  padding-top: 3rem;
  padding-bottom: 3rem;
}

.header-compact {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  margin-bottom: 2rem;
}

.header-icon {
  color: var(--accent-secondary);
}

.section-title.compact {
  margin-bottom: 0;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 1.25rem;
  max-width: 1200px;
  margin: 0 auto;
}

.project-card {
  transition: var(--transition-smooth);
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(76, 201, 240, 0.1);
  border-color: var(--accent-secondary);
}

.card-content {
  padding: 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.25rem;
}

.title-area {
  display: flex;
  align-items: center;
  gap: 0.6rem;
}

.folder-icon {
  color: var(--accent-primary);
  opacity: 0.8;
}

.project-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-primary);
}

.link-icon {
  color: var(--text-secondary);
  opacity: 0.4;
  transition: 0.3s;
}

.project-card:hover .link-icon {
  opacity: 1;
  color: var(--accent-secondary);
}

.project-role-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  background: rgba(76, 201, 240, 0.08);
  color: var(--accent-secondary);
  padding: 0.3rem 0.6rem;
  border-radius: 4px;
  font-size: 0.8rem;
  font-weight: 700;
  width: fit-content;
}

.project-desc {
  color: var(--text-secondary);
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 0.5rem;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: auto;
}

.tech-badge {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  background: rgba(67, 97, 238, 0.05);
  color: var(--accent-primary);
  padding: 0.25rem 0.6rem;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 600;
  border: 1px solid rgba(67, 97, 238, 0.15);
  transition: 0.3s;
}

.tech-badge:hover {
  background: rgba(67, 97, 238, 0.1);
  border-color: var(--accent-primary);
}

.badge-icon {
  opacity: 0.8;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  .project-desc {
    -webkit-line-clamp: 4;
    line-clamp: 4;
  }
}
</style>

