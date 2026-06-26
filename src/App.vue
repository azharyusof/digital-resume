<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { Sun, Moon, Menu, X, Terminal } from '@lucide/vue'

import ResumeHero from './components/ResumeHero.vue'
import ResumeSkills from './components/ResumeSkills.vue'
import ResumeExperience from './components/ResumeExperience.vue'
import ResumeProjects from './components/ResumeProjects.vue'
import ResumeContact from './components/ResumeContact.vue'
import ResumeContactCard from './components/ResumeContactCard.vue'

const isDarkMode = ref(true)
const isMobileMenuOpen = ref(false)
const currentHash = ref(window.location.hash)

const updateHash = () => {
  currentHash.value = window.location.hash
}

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value
  const root = document.documentElement
  if (isDarkMode.value) {
    root.classList.remove('light-mode')
    localStorage.setItem('theme', 'dark')
  } else {
    root.classList.add('light-mode')
    localStorage.setItem('theme', 'light')
  }
}

onMounted(() => {
  window.addEventListener('hashchange', updateHash)
  
  const savedTheme = localStorage.getItem('theme')
  const root = document.documentElement
  if (savedTheme === 'light') {
    isDarkMode.value = false
    root.classList.add('light-mode')
  } else {
    isDarkMode.value = true
    root.classList.remove('light-mode')
  }
})

onBeforeUnmount(() => {
  window.removeEventListener('hashchange', updateHash)
})

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}
</script>

<template>
  <div class="app-layout">
    <!-- Standalone Contact Card (Fullscreen) -->
    <ResumeContactCard v-if="currentHash === '#/contact-card'" />

    <!-- Main Resume Site -->
    <template v-else>
      <!-- Decorative Glowing Blobs (Background) -->
      <div class="glow-blob blob-1"></div>
      <div class="glow-blob blob-2"></div>

      <!-- Navigation Header -->
      <nav class="nav-bar">
        <div class="container nav-container">
          <!-- Logo -->
          <a href="#" class="logo-link">
            <Terminal :size="22" class="logo-icon" />
            <span class="logo-text">ay<span class="logo-dot">.</span>dev</span>
          </a>

          <!-- Desktop Navigation Links -->
          <div class="nav-links-desktop">
            <a href="#" class="nav-link">About</a>
            <a href="#skills" class="nav-link">Skills</a>
            <a href="#experience" class="nav-link">Experience</a>
            <a href="#projects" class="nav-link">Projects</a>
            <a href="#contact" class="nav-link">Contact</a>
          </div>

          <!-- Right Side Actions (Theme toggle + Mobile menu toggler) -->
          <div class="nav-actions">
            <button @click="toggleTheme" class="theme-toggle-btn" :aria-label="isDarkMode ? 'Switch to Light Mode' : 'Switch to Dark Mode'">
              <Sun v-if="isDarkMode" :size="20" />
              <Moon v-else :size="20" />
            </button>

            <button @click="isMobileMenuOpen = !isMobileMenuOpen" class="mobile-menu-toggle" aria-label="Toggle Menu">
              <Menu v-if="!isMobileMenuOpen" :size="22" />
              <X v-else :size="22" />
            </button>
          </div>
        </div>
      </nav>

      <!-- Mobile Drawer Menu Overlay -->
      <transition name="drawer">
        <div v-if="isMobileMenuOpen" class="mobile-drawer">
          <div class="drawer-links">
            <a href="#" @click="closeMobileMenu" class="drawer-link">About</a>
            <a href="#skills" @click="closeMobileMenu" class="drawer-link">Skills</a>
            <a href="#experience" @click="closeMobileMenu" class="drawer-link">Experience</a>
            <a href="#projects" @click="closeMobileMenu" class="drawer-link">Projects</a>
            <a href="#contact" @click="closeMobileMenu" class="drawer-link">Contact</a>
          </div>
        </div>
      </transition>

      <!-- Main Content Sections -->
      <main class="container main-content">
        <ResumeHero />
        <hr class="section-divider" />
        <ResumeSkills />
        <hr class="section-divider" />
        <ResumeExperience />
        <hr class="section-divider" />
        <ResumeProjects />
        <hr class="section-divider" />
        <ResumeContact />
      </main>

      <!-- Footer -->
      <footer class="app-footer">
        <div class="container footer-container">
          <p class="footer-copy">© 2026 Azhar Yusof. Built with Vue 3 & Vite.</p>
          <p class="footer-status">Designed for performance and responsiveness.</p>
        </div>
      </footer>
    </template>
  </div>
</template>

<style>
/* App Layout Container */
.app-layout {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Background Blurs */
.glow-blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  z-index: -1;
  opacity: 0.15;
  pointer-events: none;
}

.light-mode .glow-blob {
  opacity: 0.08;
}

.blob-1 {
  top: -10%;
  right: -5%;
  width: 500px;
  height: 500px;
  background: var(--accent-color);
  animation: float 10s ease-in-out infinite alternate;
}

.blob-2 {
  top: 40%;
  left: -10%;
  width: 600px;
  height: 600px;
  background: var(--accent-secondary);
  animation: float 12s ease-in-out infinite alternate-reverse;
}

/* Nav Bar Styles */
.nav-bar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(9, 13, 22, 0.7);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border-color);
  transition: background 0.4s, border-color 0.4s;
}

.light-mode .nav-bar {
  background: rgba(248, 250, 252, 0.75);
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;
}

.logo-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  text-decoration: none;
  color: var(--text-primary);
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: 1.25rem;
  transition: var(--transition-smooth);
}

.logo-link:hover {
  transform: translateY(-1px);
}

.logo-icon {
  color: var(--accent-color);
}

.logo-dot {
  color: var(--accent-secondary);
}

.nav-links-desktop {
  display: flex;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: var(--text-secondary);
  font-family: var(--font-heading);
  font-weight: 550;
  font-size: 0.95rem;
  transition: var(--transition-smooth);
  position: relative;
  padding: 0.25rem 0;
}

.nav-link:hover {
  color: var(--text-primary);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--gradient-accent);
  transition: var(--transition-smooth);
  border-radius: 2px;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.theme-toggle-btn {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  width: 42px;
  height: 42px;
  border-radius: 10px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition-smooth);
}

.theme-toggle-btn:hover {
  background: var(--bg-card-hover);
  border-color: var(--border-color-hover);
  transform: scale(1.05);
}

.mobile-menu-toggle {
  display: none;
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  width: 42px;
  height: 42px;
  border-radius: 10px;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  transition: var(--transition-smooth);
}

.mobile-menu-toggle:hover {
  background: var(--bg-card-hover);
  border-color: var(--border-color-hover);
}

/* Mobile Drawer Overlay */
.mobile-drawer {
  position: fixed;
  top: 70px;
  left: 0;
  width: 100%;
  height: calc(100vh - 70px);
  background: rgba(9, 13, 22, 0.95);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  z-index: 99;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-top: 1px solid var(--border-color);
}

.light-mode .mobile-drawer {
  background: rgba(248, 250, 252, 0.96);
}

.drawer-links {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  align-items: center;
}

.drawer-link {
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: 1.5rem;
  text-decoration: none;
  color: var(--text-secondary);
  transition: var(--transition-smooth);
}

.drawer-link:hover {
  color: var(--accent-color);
  transform: scale(1.08);
}

/* Section Separator */
.section-divider {
  border: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--border-color), transparent);
  margin: 1.5rem 0;
}

/* Main Container */
.main-content {
  flex-grow: 1;
}

/* Footer Section */
.app-footer {
  margin-top: auto;
  border-top: 1px solid var(--border-color);
  padding: 2.5rem 0;
  background: rgba(9, 13, 22, 0.5);
}

.light-mode .app-footer {
  background: rgba(248, 250, 252, 0.6);
}

.footer-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-copy {
  font-size: 0.9rem;
  color: var(--text-secondary);
}

.footer-status {
  font-size: 0.85rem;
  color: var(--text-muted);
}

/* Drawer Transitions */
.drawer-enter-active,
.drawer-leave-active {
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.3s;
}

.drawer-enter-from,
.drawer-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}

/* Mobile Media Queries */
@media (max-width: 968px) {
  .nav-links-desktop {
    display: none;
  }
  .mobile-menu-toggle {
    display: flex;
  }
}

@media (max-width: 576px) {
  .footer-container {
    flex-direction: column;
    text-align: center;
  }
}

/* Print CSS setup */
@media print {
  body {
    background-color: #fff !important;
    color: #000 !important;
  }
  .nav-bar, .mobile-drawer, .app-footer, .section-divider, .glow-blob {
    display: none !important;
  }
  .main-content {
    margin-top: 0 !important;
    padding-top: 0 !important;
  }
}
</style>
