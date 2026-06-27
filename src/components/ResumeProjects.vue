<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Pagination, Autoplay, Navigation } from 'swiper/modules'
import { ExternalLink, ChevronLeft, ChevronRight, X } from '@lucide/vue'

// Import Swiper styles
import 'swiper/css'
import 'swiper/css/pagination'
import 'swiper/css/navigation'

// Import assets
import blmsDashboard from '../assets/blms_dashboard.png'
import blmsList from '../assets/blms_list.png'

const activeFilter = ref('All')
const filters = ['All', 'Full-Stack', 'Frontend', 'Tools', 'DevOps']
const swiperModules = [Pagination, Autoplay, Navigation]

// Lightbox state and control logic
const selectedImage = ref(null)
const openLightbox = (img) => {
  selectedImage.value = img
  document.body.style.overflow = 'hidden' // Lock body scroll when zoom active
}
const closeLightbox = () => {
  selectedImage.value = null
  document.body.style.overflow = ''
}
const handleKeydown = (e) => {
  if (e.key === 'Escape') closeLightbox()
}
onMounted(() => window.addEventListener('keydown', handleKeydown))
onUnmounted(() => window.removeEventListener('keydown', handleKeydown))

const projects = [
  {
    title: 'Business License Management (BLMS)',
    company: 'UEM Edgenta Berhad',
    description: 'Centralized enterprise platform tracking and renewing business licenses across domestic and international UEM subsidiaries. Handles automatic expirations and multi-user verification audits.',
    category: 'Full-Stack',
    tech: ['React.js', '.NET Core', 'MSSQL', 'Chart.js', 'Bootstrap'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #6366f1, #3b82f6)',
    images: [blmsDashboard, blmsList]
  },
  {
    title: 'Workforce Management System (WMS)',
    company: 'XOX Technology Berhad',
    description: 'Enterprise team management platform for attendance logging, shift scheduling, overtime calculations, leave workflows, and analytical reporting services.',
    category: 'Full-Stack',
    tech: ['Vue.js', 'Laravel', 'MySQL', 'Tailwind CSS'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #ec4899, #8b5cf6)',
    images: []
  },
  {
    title: 'Enhanced SIRIM Label Scanner',
    company: 'XOX Technology Berhad',
    description: 'Cross-platform mobile application deployed on major stores, enabling consumers to verify product authenticity, certifications, and access detailed data sheets.',
    category: 'Frontend',
    tech: ['Flutter', '.NET 8', 'MSSQL', 'REST APIs'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #10b981, #059669)',
    images: []
  },
  {
    title: 'Vending Machine System (VMS)',
    company: 'XOX Technology Berhad',
    description: 'IoT vending machine integration managing payment gateways, digital product catalogs, remote hardware telemetry, and machine maintenance APIs.',
    category: 'Full-Stack',
    tech: ['Android Native', 'Laravel', 'MySQL', 'Java / Kotlin'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #f59e0b, #eab308)',
    images: []
  },
  {
    title: 'Travel Management (Edgenta Travel)',
    company: 'UEM Edgenta Berhad',
    description: 'Organisational travel booking portal streamlining flight, accommodation, transport scheduling, and claim workflows for corporate staff.',
    category: 'Frontend',
    tech: ['Vue.js', '.NET Core', 'MSSQL', 'Bootstrap'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #3b82f6, #06b6d4)',
    images: []
  },
  {
    title: 'DevOps & CI/CD Infrastructure',
    company: 'UEM Edgenta Berhad',
    description: 'Enterprise DevOps pipeline automating code quality audits, container builds, monitoring telemetry, security compliance, and credential storage.',
    category: 'DevOps',
    tech: ['GitHub Actions', 'Docker', 'ELK Stack', 'Grafana', 'HashiCorp Vault', 'K6', 'Playwright', 'SonarQube'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #1f2937, #111827)',
    images: []
  },
  {
    title: 'Gatepass Management System (GMS)',
    company: 'Felda Prodata System Sdn Bhd',
    description: 'Real-time monitoring and logistics control system tracking palm oil lorry movements, security clearing, and mill entry/exit gates.',
    category: 'Full-Stack',
    tech: ['.NET MVC', 'MSSQL', 'C#', 'JavaScript'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #8b5cf6, #d946ef)',
    images: []
  },
  {
    title: 'Palm Fruit Grading System',
    company: 'Felda Prodata System Sdn Bhd',
    description: 'Weighing bridge integration and fruit grading system automating thermal receipt printing and regional management reporting.',
    category: 'Tools',
    tech: ['.NET MVC', 'MSSQL', 'C#', 'Hardware Integration'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #f43f5e, #ec4899)',
    images: []
  },
  {
    title: 'FELDA GIS Plantation System',
    company: 'Felda Prodata System Sdn Bhd',
    description: 'Geospatial plantation dashboard mapping oil palm trees, asset coordinates, and residential areas in FELDA sectors.',
    category: 'Frontend',
    tech: ['React.js', 'Laravel', 'MSSQL', 'GIS / Leaflet'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #06b6d4, #10b981)',
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
      <div class="title-nav-group">
        <h2 class="section-title">Featured Projects</h2>
        
        <!-- Slider Navigation Controls -->
        <div class="slider-controls">
          <button class="slider-btn custom-proj-prev" aria-label="Previous Project">
            <ChevronLeft :size="20" />
          </button>
          <button class="slider-btn custom-proj-next" aria-label="Next Project">
            <ChevronRight :size="20" />
          </button>
        </div>
      </div>
      
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

    <!-- Projects Slider -->
    <swiper
      :key="activeFilter"
      :modules="swiperModules"
      :slides-per-view="1"
      :space-between="24"
      :pagination="{ clickable: true, el: '.projects-pagination' }"
      :navigation="{
        prevEl: '.custom-proj-prev',
        nextEl: '.custom-proj-next',
        disabledClass: 'disabled'
      }"
      :breakpoints="{
        '768': {
          slidesPerView: 2,
          spaceBetween: 24
        },
        '1100': {
          slidesPerView: 3,
          spaceBetween: 24
        }
      }"
      class="projects-swiper animate-fade-in"
    >
      <swiper-slide 
        v-for="(project, index) in filteredProjects" 
        :key="index"
      >
        <div class="glass-card project-card">
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
                :modules="[Pagination, Autoplay]"
                :slides-per-view="1"
                :loop="true"
                :autoplay="{ delay: 4000, disableOnInteraction: false }"
                :pagination="{ clickable: true }"
                class="project-image-slider"
              >
                <swiper-slide v-for="(img, imgIdx) in project.images" :key="imgIdx">
                  <img 
                    :src="img" 
                    :alt="project.title + ' screenshot ' + (imgIdx + 1)" 
                    class="project-screenshot" 
                    @click="openLightbox(img)"
                  />
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
            <div class="company-badge-wrapper">
              <span class="company-badge">{{ project.company }}</span>
            </div>
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
      </swiper-slide>
    </swiper>

    <!-- Slider Pagination Dots below carousel -->
    <div class="projects-pagination"></div>

    <!-- Lightbox Zoom Overlay Modal -->
    <transition name="fade">
      <div v-if="selectedImage" class="lightbox-overlay" @click="closeLightbox">
        <button class="lightbox-close" @click="closeLightbox" aria-label="Close image zoom">
          <X :size="24" />
        </button>
        <div class="lightbox-content" @click.stop>
          <img :src="selectedImage" alt="Enlarged screenshot" class="lightbox-image" />
        </div>
      </div>
    </transition>
  </section>
</template>

<style scoped>
.projects-section {
  padding: 3rem 0;
  position: relative;
}

.projects-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.title-nav-group {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.slider-controls {
  display: flex;
  gap: 0.75rem;
}

.slider-btn {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(8px);
}

.slider-btn:hover:not(.disabled) {
  background: var(--accent-color);
  color: #fff;
  border-color: var(--accent-color);
  box-shadow: 0 0 15px rgba(99, 102, 241, 0.4);
  transform: translateY(-2px);
}

.slider-btn.disabled {
  opacity: 0.4;
  cursor: not-allowed;
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

.projects-swiper {
  padding: 1rem 0 3rem 0; /* space for card hover and pagination */
}

.project-card {
  display: flex;
  flex-direction: column;
  padding: 0;
  overflow: hidden;
  height: 100%;
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
  height: 200px;
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
  height: 200px;
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

.project-content {
  padding: 1.5rem 1.75rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.company-badge-wrapper {
  margin-bottom: 0.5rem;
}

.company-badge {
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  opacity: 0.8;
}

.project-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 0.75rem;
}

.project-desc {
  font-size: 0.9rem;
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
  line-height: 1.6;
  flex-grow: 1;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
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

/* Main projects Swiper pagination styling */
.projects-pagination {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 1rem;
}

.projects-pagination :deep(.swiper-pagination-bullet) {
  background: var(--text-secondary);
  opacity: 0.25;
  width: 8px;
  height: 8px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.projects-pagination :deep(.swiper-pagination-bullet-active) {
  background: var(--accent-color);
  opacity: 1;
  width: 24px;
  border-radius: 4px;
  box-shadow: 0 0 10px rgba(99, 102, 241, 0.5);
}

@media print {
  .filter-bar, .slider-controls, .projects-pagination {
    display: none !important;
  }
  .project-card {
    border: 1px solid #ccc !important;
    background: transparent !important;
    box-shadow: none !important;
    page-break-inside: avoid;
  }
}

@media (max-width: 768px) {
  .projects-header {
    flex-direction: column;
    align-items: stretch;
  }
  
  .title-nav-group {
    justify-content: space-between;
  }
  
  .filter-bar {
    width: 100%;
    overflow-x: auto;
    white-space: nowrap;
    -webkit-overflow-scrolling: touch;
  }
}

/* Lightbox zoom modal styles */
.lightbox-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(10, 15, 30, 0.85);
  backdrop-filter: blur(16px);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  cursor: zoom-out;
}

.lightbox-close {
  position: absolute;
  top: 2rem;
  right: 2rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #fff;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  z-index: 2010;
}

.lightbox-close:hover {
  background: var(--accent-color);
  border-color: var(--accent-color);
  transform: rotate(90deg);
  box-shadow: 0 0 15px rgba(99, 102, 241, 0.5);
}

.lightbox-content {
  max-width: 90%;
  max-height: 90%;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: #0d121f;
  animation: zoom-in-ani 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  cursor: default;
}

.lightbox-image {
  max-width: 100%;
  max-height: 85vh;
  object-fit: contain;
  display: block;
}

/* Hover Zoom Cursor on screenshots */
.project-screenshot {
  cursor: zoom-in;
}

/* Animations */
@keyframes zoom-in-ani {
  from {
    transform: scale(0.95);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
