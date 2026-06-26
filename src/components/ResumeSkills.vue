<script setup>
import { Code, Server, Wrench } from '@lucide/vue'

const skillCategories = [
  {
    title: 'Frontend Development',
    icon: Code,
    color: 'var(--accent-color)',
    skills: [
      { name: 'Vue 3 / Composition API', level: 95 },
      { name: 'JavaScript (ES6+) / TypeScript', level: 90 },
      { name: 'HTML5 / CSS3 / SCSS', level: 90 },
      { name: 'Tailwind CSS & Responsive Design', level: 95 },
      { name: 'State Management (Pinia/Vuex)', level: 85 }
    ]
  },
  {
    title: 'Backend & Databases',
    icon: Server,
    color: 'var(--accent-secondary)',
    skills: [
      { name: 'Node.js / Express', level: 88 },
      { name: 'REST & GraphQL APIs', level: 90 },
      { name: 'PostgreSQL / MongoDB', level: 80 },
      { name: 'Redis Caching & Queues', level: 75 },
      { name: 'Firebase & Supabase', level: 85 }
    ]
  },
  {
    title: 'DevOps & Tooling',
    icon: Wrench,
    color: '#10b981', /* Emerald */
    skills: [
      { name: 'Git / GitHub Actions', level: 90 },
      { name: 'Docker & Containerization', level: 80 },
      { name: 'Vite / Webpack Build Tools', level: 88 },
      { name: 'AWS (S3, EC2, Lambda)', level: 75 },
      { name: 'Jest / Vitest / Cypress (TDD)', level: 85 }
    ]
  }
]
</script>

<template>
  <section id="skills" class="skills-section">
    <h2 class="section-title">Skills & Technologies</h2>
    <div class="grid-3 skill-categories-grid">
      <!-- Category Card -->
      <div 
        v-for="(category, index) in skillCategories" 
        :key="index" 
        class="glass-card skill-category-card"
      >
        <div class="category-header">
          <div class="category-icon-wrapper" :style="{ backgroundColor: category.color + '15', color: category.color }">
            <component :is="category.icon" :size="24" />
          </div>
          <h3>{{ category.title }}</h3>
        </div>

        <div class="skills-list">
          <div v-for="(skill, sIdx) in category.skills" :key="sIdx" class="skill-item">
            <div class="skill-info">
              <span class="skill-name">{{ skill.name }}</span>
              <span class="skill-percent">{{ skill.level }}%</span>
            </div>
            <div class="skill-bar-bg">
              <div 
                class="skill-bar-fill" 
                :style="{ width: skill.level + '%', backgroundColor: category.color }"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  padding: 3rem 0;
}

.skill-category-card {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  background-color: var(--bg-card);
}

.category-header {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.category-icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 12px;
  flex-shrink: 0;
}

.skills-list {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.skill-item {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  font-weight: 500;
}

.skill-name {
  color: var(--text-primary);
}

.skill-percent {
  color: var(--text-muted);
}

.skill-bar-bg {
  width: 100%;
  height: 6px;
  background: var(--border-color);
  border-radius: 9999px;
  overflow: hidden;
}

.skill-bar-fill {
  height: 100%;
  border-radius: 9999px;
  transition: width 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.skill-category-card:hover .skill-bar-fill {
  filter: brightness(1.1);
  box-shadow: 0 0 8px rgba(99, 102, 241, 0.3);
}

@media print {
  .skill-bar-bg {
    border: 1px solid #ccc;
    background: #f0f0f0 !important;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
  .skill-bar-fill {
    background-color: #555 !important;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
}
</style>
