<script setup>
import { Mail, MapPin, Download, Briefcase } from '@lucide/vue'

defineProps({
  name: {
    type: String,
    default: 'Noor Azhar bin Mohd Yusof'
  },
  title: {
    type: String,
    default: 'Web & Mobile Developer (Cloud & DevOps)'
  },
  location: {
    type: String,
    default: 'Selangor, MY | Kuala Lumpur, MY'
  },
  bio: {
    type: String,
    default: 'Results-driven Senior Software Engineer with comprehensive experience in developing scalable web and mobile applications. Proficient in leveraging modern frameworks and languages to build robust digital products. Demonstrated expertise in infrastructure management and deployment utilizing Docker and cloud solutions. Dedicated to driving workflow automation and integrating AI technologies to deliver high-performance software.'
  }
})

const handlePrint = () => {
  window.print()
}
</script>

<template>
  <header class="hero-section animate-fade-in-up">
    <div class="hero-container">
      <!-- Profile Avatar with Glow Effects -->
      <div class="avatar-wrapper">
        <div class="avatar-glow"></div>
        <img src="../assets/avatar.png" alt="Avatar" class="avatar-img" />
      </div>

      <!-- Intro Info -->
      <div class="hero-details">
        <div class="badge-row">
          <span class="badge">
            <Briefcase :size="14" class="icon-spacing" /> Available for Hire
          </span>
          <span class="badge location-badge">
            <MapPin :size="14" class="icon-spacing" /> {{ location }}
          </span>
        </div>

        <h1 class="gradient-text hero-name">{{ name }}</h1>
        <p class="hero-title">{{ title }}</p>
        <p class="hero-bio">{{ bio }}</p>

        <!-- Social Icons & Actions -->
        <div class="hero-actions">
          <div class="social-links">
            <a href="https://github.com/azharyusof" target="_blank" rel="noopener" class="social-icon-btn" aria-label="GitHub">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="brand-svg"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"></path><path d="M9 18c-4.51 2-5-2-7-2"></path></svg>
            </a>
            <a href="https://www.linkedin.com/in/azharyusof" target="_blank" rel="noopener" class="social-icon-btn" aria-label="LinkedIn">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="brand-svg"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect width="4" height="12" x="2" y="9"></rect><circle cx="4" cy="4" r="2"></circle></svg>
            </a>
            <a href="mailto:nazhar.myusof@gmail.com" class="social-icon-btn" aria-label="Email">
              <Mail :size="20" />
            </a>
          </div>

          <!-- <button @click="handlePrint" class="btn btn-primary print-btn">
            <Download :size="18" /> Save / Print PDF
          </button> -->
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
.hero-section {
  padding: 4rem 0 2rem;
}

.hero-container {
  display: flex;
  align-items: center;
  gap: 3.5rem;
}

.avatar-wrapper {
  position: relative;
  width: 180px;
  height: 180px;
  flex-shrink: 0;
}

.avatar-glow {
  position: absolute;
  inset: -6px;
  background: var(--gradient-accent);
  border-radius: 50%;
  filter: blur(12px);
  opacity: 0.55;
  animation: pulse-glow 3s ease-in-out infinite;
}

.avatar-img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid var(--bg-card);
  position: relative;
  z-index: 1;
  transition: var(--transition-smooth);
}

.avatar-wrapper:hover .avatar-img {
  transform: scale(1.05) rotate(2deg);
}

.hero-details {
  flex-grow: 1;
}

.badge-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-bottom: 1.25rem;
}

.icon-spacing {
  margin-right: 0.35rem;
  display: inline-block;
  vertical-align: middle;
}

.hero-name {
  margin-bottom: 0.25rem;
  font-weight: 800;
}

.hero-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 1.25rem;
}

.hero-bio {
  font-size: 1.1rem;
  color: var(--text-secondary);
  max-width: 650px;
  margin-bottom: 2rem;
  line-height: 1.6;
}

.hero-actions {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 1.5rem;
}

.social-links {
  display: flex;
  gap: 0.75rem;
}

.social-icon-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 46px;
  height: 46px;
  border-radius: 50%;
  background: var(--bg-card);
  color: var(--text-secondary);
  border: 1px solid var(--border-color);
  transition: var(--transition-smooth);
  text-decoration: none;
}

.social-icon-btn:hover {
  background: var(--bg-card-hover);
  color: var(--accent-color);
  border-color: var(--border-color-hover);
  transform: translateY(-3px) scale(1.08);
  box-shadow: 0 5px 15px var(--accent-glow);
}

/* Printing styles */
@media print {
  .hero-section {
    padding: 0;
  }
  .print-btn, .social-links {
    display: none !important;
  }
}

@media (max-width: 968px) {
  .hero-container {
    flex-direction: column;
    text-align: center;
    gap: 2rem;
  }
  .avatar-wrapper {
    width: 150px;
    height: 150px;
  }
  .badge-row {
    justify-content: center;
  }
  .hero-actions {
    justify-content: center;
    flex-direction: column;
    gap: 1.25rem;
  }
  .hero-bio {
    margin-left: auto;
    margin-right: auto;
  }
}
</style>
