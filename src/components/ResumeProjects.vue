<script setup>
import { ref, computed } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Pagination, Autoplay } from 'swiper/modules'
import { ExternalLink } from '@lucide/vue'

// Import Swiper styles
import 'swiper/css'
import 'swiper/css/pagination'

// Import assets
import blmsDashboard from '../assets/blms_dashboard.png'
import blmsList from '../assets/blms_list.png'

const activeFilter = ref('All')

const filters = ['All', 'Full-Stack', 'Frontend', 'Tools']

const swiperModules = [Pagination, Autoplay]

const projects = [
  {
    title: 'Business License Management (BLMS)',
    description: 'A centralized system for tracking, reviewing, and maintaining business licenses across domestic and international UEM Edgenta subsidiaries. Features analytics dashboards, license renewal tracking, and document downloads.',
    category: 'Full-Stack',
    tech: ['React.js', '.NET Core', 'MSSQL', 'Chart.js', 'Bootstrap'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #6366f1, #3b82f6)',
    images: [blmsDashboard, blmsList]
  },
  {
    title: 'Workforce Management System (WMS)',
    description: 'An enterprise system designed for team administration, scheduling, attendance logging, overtime computations, leave applications, and analytical reporting.',
    category: 'Full-Stack',
    tech: ['Vue.js', 'Laravel', 'MySQL', 'Tailwind CSS'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #ec4899, #8b5cf6)',
    images: []
  },
  {
    title: 'SIRIM Label Scanner Mobile App',
    description: 'A scanning and verification app deployed to Google Play Store, AppGallery, and App Store. Allows users to scan and authenticate product label details.',
    category: 'Frontend',
    tech: ['Flutter', '.NET 8', 'MSSQL', 'REST APIs'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #10b981, #059669)',
    images: []
  },
  {
    title: 'Vending Machine System (VMS)',
    description: 'An IoT vending machine management and dashboard system. Handles inventory logging, sales reporting, and vending machine telemetry APIs.',
    category: 'Tools',
    tech: ['Android Native', 'Laravel', 'MySQL', 'Java / Kotlin'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #f59e0b, #eab308)',
    images: []
  }
]

const filteredProjects = computed(() => {
  if (activeFilter.value === 'All') {
    return projects
  }
  return projects.filter(project => project.category === activeFilter.value)
})
</script>

<template>
  <section id="projects" class="projects-section">
    <div class="projects-header">
      <h2 class="section-title">Featured Projects</h2>
      
      <!-- Filter Tabs -->
      <div class="filter-bar">
        <button 
          v-for="filter in filters" 
          :key="filter"
          @click="activeFilter = filter"
          class="filter-tab"
          :class="{ active: activeFilter === filter }"
        >
          {{ filter }}
        </button>
      </div>
    </div>

    <!-- Projects Grid -->
    <div class="grid-2 projects-grid">
      <div 
        v-for="(project, index) in filteredProjects" 
        :key="index"
        class="glass-card project-card animate-fade-in"
      >
        <!-- Interactive macOS-style Browser Mockup -->
        <div class="browser-mockup">
          <div class="browser-bar">
            <span class="dot red"></span>
            <span class="dot yellow"></span>
            <span class="dot green"></span>
          </div>

          <!-- Image Slider (for cards with screenshots) -->
          <div v-if="project.images && project.images.length > 0" class="project-slider-wrapper">
            <swiper
              :modules="swiperModules"
              :slides-per-view="1"
              :loop="true"
              :autoplay="{ delay: 4000, disableOnInteraction: false }"
              :pagination="{ clickable: true }"
              class="project-image-slider"
            >
              <swiper-slide v-for="(img, imgIdx) in project.images" :key="imgIdx">
                <img :src="img" :alt="project.title + ' screenshot ' + (imgIdx + 1)" class="project-screenshot" />
              </swiper-slide>
            </swiper>
            <span class="project-category-badge">{{ project.category }}</span>
          </div>

          <!-- Solid Gradient Banner (fallback if no screenshots) -->
          <div v-else class="project-banner" :style="{ background: project.gradient }">
            <span class="project-category-badge">{{ project.category }}</span>
          </div>
        </div>

        <div class="project-content">
          <h3 class="project-title">{{ project.title }}</h3>
          <p class="project-desc">{{ project.description }}</p>

          <!-- Tech Tags -->
          <div class="tech-tags">
            <span v-for="t in project.tech" :key="t" class="tech-badge">
              {{ t }}
            </span>
          </div>

          <!-- Project Actions (Disabled/Commented as corporate applications) -->
          <!-- <div class="project-links">
            <a :href="project.githubUrl" target="_blank" rel="noopener" class="btn btn-secondary btn-sm flex-center">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="brand-svg"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"></path><path d="M9 18c-4.51 2-5-2-7-2"></path></svg> Code
            </a>
            <a :href="project.demoUrl" target="_blank" rel="noopener" class="btn btn-primary btn-sm flex-center">
              <ExternalLink :size="16" /> Demo
            </a>
          </div> -->
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects-section {
  padding: 3rem 0;
}

.projects-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.filter-bar {
  display: flex;
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  padding: 0.35rem;
  border-radius: 0.75rem;
  gap: 0.25rem;
}

.filter-tab {
  background: transparent;
  border: none;
  color: var(--text-secondary);
  padding: 0.5rem 1.25rem;
  border-radius: 0.5rem;
  font-family: var(--font-heading);
  font-weight: 600;
  font-size: 0.9rem;
  cursor: pointer;
  transition: var(--transition-smooth);
}

.filter-tab:hover {
  color: var(--accent-color);
}

.filter-tab.active {
  background: var(--accent-color);
  color: #ffffff;
}

.projects-grid {
  margin-top: 1rem;
}

.project-card {
  display: flex;
  flex-direction: column;
  padding: 0;
  overflow: hidden;
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), box-shadow 0.4s cubic-bezier(0.16, 1, 0.3, 1), border-color 0.4s ease;
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 30px rgba(99, 102, 241, 0.15);
  border-color: rgba(99, 102, 241, 0.3);
}

.browser-mockup {
  width: 100%;
  position: relative;
  border-bottom: 1px solid var(--border-color);
  background: #0f172a;
  overflow: hidden;
}

.light-mode .browser-mockup {
  background: #f1f5f9;
}

.browser-bar {
  height: 32px;
  padding: 0 1rem;
  display: flex;
  align-items: center;
  gap: 6px;
  border-bottom: 1px solid var(--border-color);
  background: rgba(15, 23, 42, 0.6);
  backdrop-filter: blur(10px);
}

.light-mode .browser-bar {
  background: rgba(241, 245, 249, 0.8);
}

.dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  display: inline-block;
  opacity: 0.8;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.project-card:hover .dot {
  opacity: 1;
}

.project-card:hover .dot.red {
  transform: scale(1.1);
}

.dot.red { background-color: #ef4444; }
.dot.yellow { background-color: #f59e0b; }
.dot.green { background-color: #10b981; }

.project-slider-wrapper {
  position: relative;
  height: 220px;
  width: 100%;
  overflow: hidden;
}

.project-image-slider {
  width: 100%;
  height: 100%;
}

.project-screenshot {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  display: block;
  transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1), filter 0.5s ease;
  filter: saturate(0.9) brightness(0.95);
}

.project-card:hover .project-screenshot {
  transform: scale(1.04);
  filter: saturate(1.05) brightness(1.02);
}

.project-banner {
  height: 220px;
  width: 100%;
  position: relative;
  transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1), filter 0.5s ease;
}

.project-card:hover .project-banner {
  transform: scale(1.04);
  filter: saturate(1.2) brightness(1.05);
}

.project-category-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(0, 0, 0, 0.55);
  color: #fff;
  font-size: 0.75rem;
  font-weight: 600;
  padding: 0.25rem 0.75rem;
  border-radius: 9999px;
  backdrop-filter: blur(4px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  z-index: 10;
}

/* Custom Swiper Pagination Styles inside project cards */
.project-image-slider :deep(.swiper-pagination-bullet) {
  background: #fff;
  opacity: 0.4;
  width: 7px;
  height: 7px;
  transition: all 0.3s ease;
}

.project-image-slider :deep(.swiper-pagination-bullet-active) {
  background: var(--accent-color);
  opacity: 1;
  width: 20px;
  border-radius: 4px;
}

.project-content {
  padding: 1.75rem 2rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.project-title {
  font-size: 1.3rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 0.75rem;
}

.project-desc {
  font-size: 0.95rem;
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
  line-height: 1.6;
  flex-grow: 1;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.75rem;
}

.tech-badge {
  font-size: 0.75rem;
  font-weight: 600;
  background: var(--bg-badge);
  color: var(--accent-color);
  padding: 0.25rem 0.6rem;
  border-radius: 6px;
  border: 1px solid rgba(99, 102, 241, 0.1);
}

.project-links {
  display: flex;
  gap: 1rem;
}

.btn-sm {
  padding: 0.5rem 1rem;
  font-size: 0.85rem;
  border-radius: 0.5rem;
}

.flex-center {
  display: flex;
  align-items: center;
  gap: 0.35rem;
}

@media print {
  .filter-bar, .project-links {
    display: none !important;
  }
  .project-card {
    border: 1px solid #ccc !important;
    background: transparent !important;
    box-shadow: none !important;
    page-break-inside: avoid;
  }
  .project-banner {
    height: 60px !important;
    border-bottom: 1px solid #ccc;
  }
}

@media (max-width: 576px) {
  .projects-header {
    flex-direction: column;
    align-items: flex-start;
  }
  .filter-bar {
    width: 100%;
    overflow-x: auto;
  }
  .filter-tab {
    flex-grow: 1;
    text-align: center;
  }
}
</style>
