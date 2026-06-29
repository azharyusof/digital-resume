<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Pagination, Navigation } from 'swiper/modules'
import { Cloud, Cpu, Network, Award, ExternalLink, Calendar, FileText, ChevronLeft, ChevronRight } from '@lucide/vue'

// Import Swiper styles
import 'swiper/css'
import 'swiper/css/pagination'
import 'swiper/css/navigation'

const swiperModules = [Pagination, Navigation]

const certificates = [
  {
    title: 'Microsoft Azure Solution Architect Expert',
    issuer: 'Microsoft',
    issueDate: 'May 2024',
    credentialId: '683FDBDB1A1321DC',
    link: 'https://aws.amazon.com/',
    icon: Cloud,
    color: '#3b82f6', /* Blue */
    theme: 'Cloud Solutions Architecture'
  },
  {
    title: 'Microsoft Azure Security Engineer Associate',
    issuer: 'Microsoft',
    issueDate: 'April 2024',
    credentialId: '52D5C712C72FAD28',
    link: 'https://cloud.google.com/',
    icon: Cpu,
    color: '#ec4899', /* Pink/Magenta */
    theme: 'Cloud Security'
  },
  {
    title: 'Microsoft Azure Administrator Associate',
    issuer: 'Microsoft',
    issueDate: 'April 2024',
    credentialId: '66FB193C89519CFC',
    link: 'https://www.sap.com/',
    icon: Network,
    color: '#10b981', /* Emerald */
    theme: 'Cloud Administration'
  },
  {
    title: 'Android Mobile Application Developer',
    issuer: 'IEEE Malaysia',
    issueDate: 'November 2013',
    credentialId: '-',
    link: 'https://www.mbot.org.my/',
    icon: Network,
    color: '#10b981', /* Emerald */
    theme: 'Mobile Development'
  },
  {
    title: 'Graduate Technologist',
    issuer: 'Malaysia Board of Technologists (MBOT)',
    issueDate: 'December 2024',
    credentialId: 'GT24120135',
    link: 'https://www.mbot.org.my/',
    icon: Network,
    color: '#10b981', /* Emerald */
    theme: 'Professional Membership'
  },
  {
    title: 'Digital Leadership',
    issuer: 'Peoplelogy Berhad & Yayasan Peneraju',
    issueDate: 'January 2024',
    credentialId: '-',
    link: 'https://www.mbot.org.my/',
    icon: Network,
    color: '#10b981', /* Emerald */
    theme: 'Leadership Development'
  }
]
</script>

<template>
  <section id="certificates" class="certificates-section">
    <div class="section-header">
      <h2 class="section-title">Professional Certificates</h2>
      <!-- <div class="slider-controls">
        <button class="custom-prev-btn" aria-label="Previous slide">
          <ChevronLeft :size="20" />
        </button>
        <button class="custom-next-btn" aria-label="Next slide">
          <ChevronRight :size="20" />
        </button>
      </div> -->
    </div>

    <!-- Swiper Slider Container -->
    <swiper
      :modules="swiperModules"
      :slides-per-view="1"
      :space-between="24"
      :pagination="{ clickable: true }"
      :navigation="{
        prevEl: '.custom-prev-btn',
        nextEl: '.custom-next-btn'
      }"
      :breakpoints="{
        '768': {
          slidesPerView: 2,
          spaceBetween: 24,
        },
        '1024': {
          slidesPerView: 3,
          spaceBetween: 24,
        }
      }"
      class="certificates-slider"
    >
      <swiper-slide v-for="(cert, index) in certificates" :key="index">
        <!-- Certificate Glass Card -->
        <div class="glass-card certificate-card">
          <!-- Card Banner Area -->
          <div class="cert-theme-banner" :style="{ background: cert.color + '15', borderBottom: '1px solid ' + cert.color + '25' }">
            <span class="cert-theme-tag" :style="{ color: cert.color, backgroundColor: cert.color + '10' }">
              {{ cert.theme }}
            </span>
          </div>

          <div class="cert-card-content">
            <!-- Header: Organization Icon & Name -->
            <div class="cert-header">
              <div class="cert-icon-box" :style="{ backgroundColor: cert.color + '15', color: cert.color }">
                <component :is="cert.icon" :size="24" />
              </div>
              <div class="cert-title-block">
                <h3 class="cert-name">{{ cert.title }}</h3>
                <span class="cert-issuer">{{ cert.issuer }}</span>
              </div>
            </div>

            <!-- Body: Date and ID -->
            <div class="cert-metadata">
              <div class="meta-item">
                <Calendar :size="14" class="meta-icon" />
                <span>Issued: <strong>{{ cert.issueDate }}</strong></span>
              </div>
              <div class="meta-item">
                <FileText :size="14" class="meta-icon" />
                <span>Credential ID: <strong>{{ cert.credentialId }}</strong></span>
              </div>
            </div>

            <!-- Footer Link -->
            <!-- <div class="cert-footer">
              <a :href="cert.link" target="_blank" rel="noopener" class="btn btn-secondary cert-link-btn">
                <Award :size="16" />
                <span>View Credential</span>
                <ExternalLink :size="14" class="link-arrow" />
              </a>
            </div> -->
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </section>
</template>

<style scoped>
.certificates-section {
  padding: 3rem 0;
}

.section-lead {
  font-size: 1.1rem;
  color: var(--text-secondary);
  max-width: 700px;
  margin-bottom: 2.5rem;
  line-height: 1.6;
}

.certificates-slider {
  padding: 1rem 0 3.5rem; /* Extra bottom padding for pagination dots */
  margin: 0 -0.5rem;
}

.certificates-slider :deep(.swiper-slide) {
  height: auto; /* Allow slides to match tallest element height */
  display: flex;
}

.certificate-card {
  width: 100%;
  padding: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  height: 100%;
  border-radius: 1.25rem;
  background-color: var(--bg-card);
}

.cert-theme-banner {
  padding: 0.75rem 1.5rem;
  display: flex;
  align-items: center;
}

.cert-theme-tag {
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.25rem 0.65rem;
  border-radius: 6px;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

.cert-card-content {
  padding: 1.75rem 1.5rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  gap: 1.5rem;
}

.cert-header {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
}

.cert-icon-box {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.cert-title-block {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.cert-name {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-primary);
  line-height: 1.35;
}

.cert-issuer {
  font-size: 0.85rem;
  font-weight: 550;
  color: var(--text-muted);
}

.cert-metadata {
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
  background: rgba(0, 0, 0, 0.1);
  padding: 1rem;
  border-radius: 0.75rem;
  border: 1px solid var(--border-color);
}

.light-mode .cert-metadata {
  background: rgba(0, 0, 0, 0.02);
}

.meta-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.85rem;
  color: var(--text-secondary);
}

.meta-icon {
  color: var(--accent-color);
  flex-shrink: 0;
}

.cert-footer {
  margin-top: auto;
}

.cert-link-btn {
  width: 100%;
  justify-content: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  border-radius: 0.75rem;
}

.link-arrow {
  transition: transform 0.3s ease;
}

.cert-link-btn:hover .link-arrow {
  transform: translate(2px, -2px);
}

/* Custom Navigation Controls in Header */
.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.section-header .section-title {
  margin-bottom: 0;
}

.slider-controls {
  display: flex;
  gap: 0.75rem;
}

.custom-prev-btn,
.custom-next-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  cursor: pointer;
  transition: var(--transition-smooth);
}

.custom-prev-btn:hover,
.custom-next-btn:hover {
  background: var(--bg-card-hover);
  color: var(--accent-color);
  border-color: var(--border-color-hover);
  box-shadow: 0 0 12px var(--accent-glow);
  transform: scale(1.05);
}

/* Swiper disabled buttons styling */
.swiper-button-disabled,
.custom-prev-btn:disabled,
.custom-next-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
  pointer-events: none;
}

:deep(.swiper-pagination-bullet) {
  background: var(--text-muted);
  opacity: 0.3;
  width: 8px;
  height: 8px;
  transition: var(--transition-smooth);
}

:deep(.swiper-pagination-bullet-active) {
  background: var(--accent-color);
  opacity: 1;
  width: 24px;
  border-radius: 4px;
  box-shadow: 0 0 8px var(--accent-glow);
}

@media print {
  .certificates-section {
    padding: 0;
    page-break-inside: avoid;
  }
  .certificates-slider {
    padding-bottom: 0 !important;
  }
  .slider-controls,
  :deep(.swiper-pagination) {
    display: none !important;
  }
  .certificate-card {
    border: 1px solid #ccc !important;
    background: transparent !important;
    box-shadow: none !important;
  }
}

@media (max-width: 768px) {
  .slider-controls {
    display: none !important; /* Hide arrows on mobile for swipe only */
  }
}
</style>
