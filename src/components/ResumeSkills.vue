<script setup>
import { Code, Server, Wrench } from '@lucide/vue'

const skillCategories = [
  {
    title: 'Frontend & Mobile',
    icon: Code,
    color: 'var(--accent-color)',
    skills: [
      { name: 'Vue.js (Composition API)', level: 95 },
      { name: 'React.js / JavaScript (ES6+)', level: 90 },
      { name: 'Flutter (Mobile Development)', level: 85 },
      { name: 'Android Native Development', level: 80 },
      { name: 'HTML5 / CSS3 / Responsive Layouts', level: 90 }
    ]
  },
  {
    title: 'Backend & Databases',
    icon: Server,
    color: 'var(--accent-secondary)',
    skills: [
      { name: 'Laravel (PHP)', level: 90 },
      { name: '.NET Core / .NET 8 / ASP.NET MVC', level: 90 },
      { name: 'MySQL', level: 88 },
      { name: 'Microsoft SQL Server (MSSQL)', level: 88 },
      { name: 'Web / RESTful API Integrations', level: 92 }
    ]
  },
  {
    title: 'DevOps & QA',
    icon: Wrench,
    color: '#10b981', /* Emerald */
    skills: [
      { name: 'CI/CD (GitHub Actions / Git)', level: 92 },
      { name: 'Docker & Containerization', level: 85 },
      { name: 'Monitoring (ELK Stack & Grafana)', level: 80 },
      { name: 'Automated Testing (Playwright / K6)', level: 82 },
      { name: 'SecOps (HashiCorp Vault / SonarQube)', level: 80 }
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
