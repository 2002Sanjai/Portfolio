<script setup>
import { ref } from 'vue'
import { Briefcase, Building, Calendar, CircleChevronRight } from 'lucide-vue-next'

const experiences = ref([
  {
    company: 'Vibrace Technology',
    role: 'Frontend Developer',
    period: '24 Mar 2025 - present',
    highlights: [
      'Spearheading front-end architecture and UI/UX implementation.',
      'Collaborating across teams to drive successful project completion.'
    ]
  },
  {
    company: 'Green Info. Tech.',
    role: 'Frontend Developer',
    period: '22 Jun 2023 – 22 Jun 2024',
    highlights: [
      'Developed and maintained highly scalable web applications using Vue.js and React.js.',
      'Integrated complex APIs and minimized bugs through rigorous testing paradigms.',
      'Mentored team members and utilized agile methodologies via Jira.'
    ]
  }
])
</script>

<template>
  <section id="experience" class="section experience">
    <h2 class="section-title">Professional Experience</h2>
    <div class="timeline">
      <div v-for="(exp, index) in experiences" :key="index" class="timeline-item glass-panel">
        <div class="timeline-header">
          <div class="exp-info">
            <div class="role-wrapper">
              <Briefcase class="icon-accent" :size="22" />
              <h3 class="role">{{ exp.role }}</h3>
            </div>
            <div class="company-wrapper">
              <Building class="icon-secondary" :size="18" />
              <h4 class="company">{{ exp.company }}</h4>
            </div>
          </div>
          <span class="period">
            <Calendar :size="14" />
            {{ exp.period }}
          </span>
        </div>
        <ul class="highlights">
          <li v-for="(point, pIndex) in exp.highlights" :key="pIndex">
            <CircleChevronRight class="bullet-icon" :size="16" />
            {{ point }}
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>


<style scoped>
.timeline {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 900px;
  margin: 0 auto;
}

.timeline-item {
  padding: 1.5rem;
  text-align: left;
  position: relative;
  transition: var(--transition-smooth);
}

.timeline-item:hover {
  transform: translateX(10px);
  border-left: 4px solid var(--accent-primary);
  box-shadow: 0 10px 30px rgba(67, 97, 238, 0.05);
}

.timeline-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.5rem;
  border-bottom: 1px solid var(--border-light);
  padding-bottom: 1rem;
}

.exp-info {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.role-wrapper, .company-wrapper {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.icon-accent {
  color: var(--accent-primary);
}

.icon-secondary {
  color: var(--accent-secondary);
}

.role {
  font-size: 1.25rem;
  color: var(--text-primary);
  font-weight: 700;
}

.company {
  font-size: 1rem;
  color: var(--accent-secondary);
  font-weight: 600;
}

.period {
  font-size: 0.9rem;
  color: var(--text-secondary);
  background: rgba(255, 255, 255, 0.05);
  padding: 0.4rem 1rem;
  border-radius: 20px;
  white-space: nowrap;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.highlights {
  list-style: none;
  padding-left: 0;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.highlights li {
  display: flex;
  align-items: flex-start;
  gap: 0.8rem;
  color: var(--text-secondary);
  font-size: 1.05rem;
  line-height: 1.6;
}

.bullet-icon {
  color: var(--accent-primary);
  margin-top: 0.25rem;
  flex-shrink: 0;
}


@media (max-width: 768px) {
  .timeline-header {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
