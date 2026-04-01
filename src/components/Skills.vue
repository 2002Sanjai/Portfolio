<script setup>
import { ref, markRaw } from 'vue'
import { 
  Layout, Layers, Server, Database, Wrench,
  Atom, Box, Code, FileCode, FileJson, Globe, Hash, 
  Github, Gitlab, Kanban, Palette, PenTool, Send 
} from 'lucide-vue-next'

const skillCategories = ref([
  {
    title: 'Frontend Frameworks',
    icon: markRaw(Layout),
    skills: [
      { name: 'Vue.js', icon: markRaw(Code) },
      { name: 'React.js', icon: markRaw(Atom) },
      { name: 'HTML5', icon: markRaw(FileCode) },
      { name: 'CSS3', icon: markRaw(Palette) },
      { name: 'JavaScript', icon: markRaw(FileJson) }
    ]
  },
  {
    title: 'State Management',
    icon: markRaw(Layers),
    skills: [
      { name: 'Pinia', icon: markRaw(Box) },
      { name: 'Vuex', icon: markRaw(Layers) }
    ]
  },
  {
    title: 'Backend & APIs',
    icon: markRaw(Server),
    skills: [
      { name: 'Node.js', icon: markRaw(Server) },
      { name: 'RESTful APIs', icon: markRaw(Globe) }
    ]
  },
  {
    title: 'Databases',
    icon: markRaw(Database),
    skills: [
      { name: 'MySQL', icon: markRaw(Database) },
      { name: 'MongoDB', icon: markRaw(Hash) }
    ]
  },
  {
    title: 'Tools & Utilities',
    icon: markRaw(Wrench),
    skills: [
      { name: 'GitHub', icon: markRaw(Github) },
      { name: 'GitLab', icon: markRaw(Gitlab) },
      { name: 'Postman', icon: markRaw(Send) },
      { name: 'draw.io', icon: markRaw(PenTool) },
      { name: 'JIRA', icon: markRaw(Kanban) }
    ]
  }
])
</script>

<template>
  <section id="skills" class="section skills">
    <h2 class="section-title">Technical Proficiencies</h2>
    <div class="skills-grid">
      <div v-for="(category, index) in skillCategories" :key="index" class="skill-category glass-panel">
        <div class="category-header">
          <component :is="category.icon" class="category-icon" :size="20" />
          <h3 class="category-title">{{ category.title }}</h3>
        </div>
        <ul class="skill-list">
          <li v-for="(skill, sIndex) in category.skills" :key="sIndex" class="skill-item">
            <component :is="skill.icon" class="skill-icon" :size="14" />
            {{ skill.name }}
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>



<style scoped>
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1.25rem;
  width: 100%;
}

.skill-category {
  padding: 1rem;
  transition: var(--transition-smooth);
}

.skill-category:hover {
  transform: translateY(-3px);
  border-color: var(--accent-primary);
  box-shadow: 0 5px 20px rgba(67, 97, 238, 0.08);
}

.category-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 1rem;
  padding-bottom: 0.6rem;
  border-bottom: 1px solid var(--border-light);
}

.category-icon {
  color: var(--accent-primary);
}

.category-title {
  font-size: 1rem;
  font-weight: 700;
  color: var(--text-primary);
}


.skill-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.skill-item {
  background: rgba(255, 255, 255, 0.04);
  padding: 0.4rem 0.9rem;
  border-radius: 30px;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--text-secondary);
  border: 1px solid rgba(255, 255, 255, 0.04);
  transition: var(--transition-smooth);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: default;
}

.skill-icon {
  opacity: 0.6;
  transition: var(--transition-smooth);
}

.skill-item:hover {
  color: var(--accent-secondary);
  border-color: var(--accent-secondary);
  background: rgba(76, 201, 240, 0.04);
  transform: translateY(-2px);
  box-shadow: 0 4px 10px rgba(76, 201, 240, 0.15);
}

.skill-item:hover .skill-icon {
  opacity: 1;
  color: var(--accent-secondary);
  transform: scale(1.1);
}


</style>
