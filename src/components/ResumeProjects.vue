<script setup>
import { ref, computed } from 'vue'
import { ExternalLink } from '@lucide/vue'

const activeFilter = ref('All')

const filters = ['All', 'Full-Stack', 'Frontend', 'Tools']

const projects = [
  {
    title: 'PulseSync Cloud Dashboard',
    description: 'A real-time monitoring and server status platform. Features dynamic charts, low-latency metrics collection via WebSockets, and alert notification configurations.',
    category: 'Full-Stack',
    tech: ['Vue 3', 'Node.js', 'Socket.io', 'Chart.js', 'PostgreSQL'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #6366f1, #3b82f6)'
  },
  {
    title: 'Kroma UI Design Kit',
    description: 'An open-source, highly accessible Tailwind-compatible component library for Vue developers. Reusable, themeable, and WCAG compliant.',
    category: 'Frontend',
    tech: ['Vue 3', 'Tailwind CSS', 'Vite', 'Storybook'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #ec4899, #8b5cf6)'
  },
  {
    title: 'Taskly Flow Manager',
    description: 'A beautiful drag-and-drop Kanban workspace featuring offline data persistence, keyboard shortcuts, and team workspace synchronization.',
    category: 'Frontend',
    tech: ['Vue 3', 'Pinia', 'HTML5 Drag & Drop', 'IndexedDB'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #10b981, #059669)'
  },
  {
    title: 'MiniGit Automation CLI',
    description: 'A CLI automation wizard that optimizes git branching workflows, triggers CI/CD build scripts, and manages remote release deployments.',
    category: 'Tools',
    tech: ['Node.js', 'Commander.js', 'Inquirer', 'ShellJS'],
    demoUrl: 'https://example.com',
    githubUrl: 'https://github.com',
    gradient: 'linear-gradient(135deg, #f59e0b, #eab308)'
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
        <!-- Project Accent Banner -->
        <div class="project-banner" :style="{ background: project.gradient }">
          <span class="project-category-badge">{{ project.category }}</span>
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

          <!-- Project Actions -->
          <div class="project-links">
            <a :href="project.githubUrl" target="_blank" rel="noopener" class="btn btn-secondary btn-sm flex-center">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="brand-svg"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"></path><path d="M9 18c-4.51 2-5-2-7-2"></path></svg> Code
            </a>
            <a :href="project.demoUrl" target="_blank" rel="noopener" class="btn btn-primary btn-sm flex-center">
              <ExternalLink :size="16" /> Demo
            </a>
          </div>
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
}

.project-banner {
  height: 120px;
  width: 100%;
  position: relative;
  transition: var(--transition-smooth);
}

.project-category-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(0, 0, 0, 0.45);
  color: #fff;
  font-size: 0.75rem;
  font-weight: 600;
  padding: 0.25rem 0.75rem;
  border-radius: 9999px;
  backdrop-filter: blur(4px);
  border: 1px solid rgba(255, 255, 255, 0.15);
}

.project-card:hover .project-banner {
  filter: saturate(1.2) brightness(1.05);
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
