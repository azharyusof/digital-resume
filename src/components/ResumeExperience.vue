<script setup>
import { Calendar, MapPin, Building } from '@lucide/vue'

const experiences = [
  {
    role: 'Senior Full-Stack Engineer',
    company: 'InnovateTech Solutions',
    period: '2023 - Present',
    location: 'San Francisco, CA (Remote)',
    bullets: [
      'Architected and co-developed a multi-tenant SaaS admin portal using Vue 3 (Composition API, Pinia) and Node.js, improving page performance by 40%.',
      'Led a team of 4 frontend engineers to rebuild legacy apps, implementing a shared custom UI library reducing layout design-to-dev time by 50%.',
      'Designed scalable database schemas in PostgreSQL and integrated Redis caching, resulting in a 30% reduction in query latencies.'
    ]
  },
  {
    role: 'Full-Stack Developer',
    company: 'Skyward Software Lab',
    period: '2021 - 2023',
    location: 'Austin, TX (Hybrid)',
    bullets: [
      'Built responsive client dashboards using Vue 2/3 and RESTful API integrations with Express.',
      'Maintained and optimized CI/CD workflows utilizing GitHub Actions, cutting build-to-deploy pipeline times by 15 minutes.',
      'Integrated Stripe payments and automated subscription billing workflows, growing checkout conversions by 12%.'
    ]
  },
  {
    role: 'Frontend Developer',
    company: 'PixelPerfect Web Agency',
    period: '2019 - 2021',
    location: 'San Jose, CA',
    bullets: [
      'Developed 20+ pixel-perfect client marketing sites and web apps using CSS grid, vanilla JS, and Vue.',
      'Collaborated closely with designers using Figma to refine UX flow, lowering user bounce rates by an average of 18%.',
      'Optimized image loaders, fonts, and assets for fast loading speed, scoring 95+ on Google Lighthouse audits.'
    ]
  }
]
</script>

<template>
  <section id="experience" class="experience-section">
    <h2 class="section-title">Work Experience</h2>
    
    <div class="timeline-container">
      <div v-for="(job, index) in experiences" :key="index" class="timeline-item">
        <!-- Timeline track line and dot -->
        <div class="timeline-marker">
          <div class="marker-dot"></div>
          <div class="marker-line" v-if="index < experiences.length - 1"></div>
        </div>

        <!-- Experience details glass card -->
        <div class="glass-card timeline-card">
          <div class="card-header">
            <div class="job-meta">
              <h3 class="role-title">{{ job.role }}</h3>
              <div class="company-row">
                <span class="company-name">
                  <Building :size="14" class="icon-spacing" /> {{ job.company }}
                </span>
                <span class="job-date">
                  <Calendar :size="14" class="icon-spacing" /> {{ job.period }}
                </span>
                <span class="job-location">
                  <MapPin :size="14" class="icon-spacing" /> {{ job.location }}
                </span>
              </div>
            </div>
          </div>

          <!-- Bullet Points -->
          <ul class="achievements-list">
            <li v-for="(bullet, bIdx) in job.bullets" :key="bIdx">
              {{ bullet }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.experience-section {
  padding: 3rem 0;
}

.timeline-container {
  display: flex;
  flex-direction: column;
  position: relative;
  padding-left: 2rem;
  margin-top: 1rem;
}

.timeline-item {
  display: flex;
  position: relative;
  padding-bottom: 2.5rem;
}

.timeline-item:last-child {
  padding-bottom: 0;
}

/* Timeline vertical line indicator */
.timeline-marker {
  position: absolute;
  left: -2rem;
  top: 0;
  bottom: 0;
  width: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.marker-dot {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--bg-app);
  border: 3px solid var(--accent-color);
  z-index: 2;
  transition: var(--transition-smooth);
}

.marker-line {
  flex-grow: 1;
  width: 2px;
  background: var(--border-color);
  z-index: 1;
  transition: var(--transition-smooth);
}

/* Connect interactions on hover */
.timeline-item:hover .marker-dot {
  transform: scale(1.3);
  border-color: var(--accent-secondary);
  box-shadow: 0 0 10px var(--accent-secondary);
}

.timeline-item:hover .marker-line {
  background: var(--accent-color);
}

.timeline-card {
  width: 100%;
  padding: 1.75rem 2rem;
}

.card-header {
  margin-bottom: 1.25rem;
}

.role-title {
  font-size: 1.3rem;
  color: var(--text-primary);
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.company-row {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  font-size: 0.85rem;
  color: var(--text-muted);
}

.company-name {
  color: var(--accent-color);
  font-weight: 550;
}

.icon-spacing {
  margin-right: 0.25rem;
  display: inline-block;
  vertical-align: middle;
}

.achievements-list {
  list-style-type: none;
  padding-left: 0;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.achievements-list li {
  position: relative;
  padding-left: 1.25rem;
  font-size: 0.95rem;
  color: var(--text-secondary);
}

.achievements-list li::before {
  content: "•";
  position: absolute;
  left: 0.25rem;
  color: var(--accent-color);
  font-weight: bold;
}

@media print {
  .timeline-container {
    padding-left: 0;
  }
  .timeline-marker {
    display: none;
  }
  .timeline-card {
    border: none !important;
    background: transparent !important;
    box-shadow: none !important;
    padding: 1rem 0 !important;
  }
  .timeline-item {
    padding-bottom: 1.5rem;
    page-break-inside: avoid;
  }
}

@media (max-width: 768px) {
  .company-row {
    flex-direction: column;
    gap: 0.35rem;
  }
}
</style>
