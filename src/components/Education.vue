<script setup>
import { ref } from 'vue'
import { GraduationCap, Building2, Calendar, Trophy } from 'lucide-vue-next'

const education = ref([
  {
    degree: 'B.E Computer Science and Engineering',
    institution: 'Prince Shri Venkateshwara Padmavathy Engineering College',
    score: '8.05 CGPA',
    period: '2019 - 2023'
  },
  {
    degree: 'Higher Secondary School (+2)',
    institution: 'Sri Vivekanandha Hr. Sec. School',
    score: '74%',
    period: '2019'
  },
  {
    degree: 'Secondary School (SSLC)',
    institution: 'Sri Vivekanandha Hr. Sec. School',
    score: '94%',
    period: '2017'
  }
])
</script>


<template>
  <section id="education" class="section education">
    <h2 class="section-title">Education</h2>
    <div class="timeline">
      <div v-for="(edu, index) in education" :key="index" class="timeline-item glass-panel">
        <div class="timeline-header">
          <div class="edu-info">
            <div class="role-wrapper">
              <GraduationCap class="icon-accent" :size="24" />
              <h3 class="role">{{ edu.degree }}</h3>
            </div>
            <div class="company-wrapper">
              <Building2 :size="18" class="icon-secondary" />
              <h4 class="company">{{ edu.institution }}</h4>
            </div>
          </div>
          <div class="meta-info">
            <span class="period">
              <Calendar :size="14" />
              {{ edu.period }}
            </span>
            <span class="score">
              <Trophy :size="14" />
              {{ edu.score }}
            </span>
          </div>
        </div>
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
  border-left: 4px solid var(--accent-secondary);
  box-shadow: 0 10px 30px rgba(76, 201, 240, 0.05);
}

.timeline-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  width: 100%;
}

.edu-info {
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
  color: var(--text-secondary);
  font-weight: 500;
}

.meta-info {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.5rem;
}

.period {
  font-size: 0.9rem;
  color: var(--text-secondary);
  background: rgba(255, 255, 255, 0.05);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  white-space: nowrap;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.score {
  font-size: 1rem;
  color: var(--accent-primary);
  background: rgba(67, 97, 238, 0.1);
  padding: 0.4rem 1rem;
  border-radius: 20px;
  font-weight: 600;
  white-space: nowrap;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}


@media (max-width: 768px) {
  .timeline-header {
    flex-direction: column;
    gap: 1rem;
  }
  .meta-info {
    align-items: flex-start;
    flex-direction: row;
  }
}
</style>
