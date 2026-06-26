<script setup>
import { Mail, Phone, MapPin, ArrowLeft, Download, Check, MessageSquare } from '@lucide/vue'
import { ref } from 'vue'

const name = 'Azhar Yusof'
const title = 'Assistant Team Lead, Software R&D'
const company = 'XOX Technology Berhad'
const email = 'nazhar.myusof@gmail.com'
const phone = '(+60) 19-687 0771'
const rawPhone = '+60196870771'
const location = 'Selangor, Malaysia'

const isSaved = ref(false)

const handleSaveContact = () => {
  // Construct vCard data
  const vcard = `BEGIN:VCARD
VERSION:3.0
N:Yusof;Azhar;;;
FN:Azhar Yusof
ORG:${company}
TITLE:${title}
TEL;TYPE=CELL,VOICE:${rawPhone}
EMAIL;TYPE=PREF,INTERNET:${email}
ADR;TYPE=HOME:;;Bandar Puncak Alam;Selangor;;Malaysia
URL:https://github.com/azharyusof/digital-resume
END:VCARD`

  // Generate blob and trigger download
  const blob = new Blob([vcard], { type: 'text/vcard;charset=utf-8;' })
  const url = URL.createObjectURL(blob)
  const link = document.createElement('a')
  link.href = url
  link.download = 'Azhar_Yusof_Contact.vcf'
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
  URL.revokeObjectURL(url)

  isSaved.value = true
  setTimeout(() => {
    isSaved.value = false
  }, 3000)
}
</script>

<template>
  <div class="card-screen animate-fade-in">
    <!-- Back Button -->
    <a href="#" class="back-link">
      <ArrowLeft :size="16" /> Back to Resume
    </a>

    <!-- Virtual Business Card Panel -->
    <div class="glass-card business-card-panel">
      <!-- Card Header -->
      <div class="card-profile">
        <div class="avatar-glow"></div>
        <img src="../assets/avatar.png" alt="Azhar Yusof" class="profile-img" />
        
        <h2 class="profile-name">{{ name }}</h2>
        <p class="profile-title">{{ title }}</p>
        <p class="profile-company">{{ company }}</p>
        
        <span class="location-badge">
          <MapPin :size="14" class="icon-spacing" /> {{ location }}
        </span>
      </div>

      <!-- Action Buttons -->
      <div class="actions-group">
        <!-- Save to Contacts (vCard) -->
        <button @click="handleSaveContact" class="btn btn-primary save-contact-btn" :class="{ success: isSaved }">
          <component :is="isSaved ? Check : Download" :size="18" />
          {{ isSaved ? 'Saved to Downloads!' : 'Add to Contacts' }}
        </button>

        <!-- Direct Communication Options -->
        <div class="communication-grid">
          <a :href="'tel:' + rawPhone" class="communication-btn" title="Call Mobile">
            <div class="comm-icon-box call-color">
              <Phone :size="20" />
            </div>
            <span>Call</span>
          </a>

          <a :href="'https://wa.me/' + rawPhone.replace('+', '')" target="_blank" rel="noopener" class="communication-btn" title="WhatsApp Chat">
            <div class="comm-icon-box whatsapp-color">
              <MessageSquare :size="20" />
            </div>
            <span>WhatsApp</span>
          </a>

          <a :href="'mailto:' + email" class="communication-btn" title="Send Email">
            <div class="comm-icon-box email-color">
              <Mail :size="20" />
            </div>
            <span>Email</span>
          </a>
        </div>
      </div>

      <!-- Social & Repository Links -->
      <div class="social-links-footer">
        <a href="https://github.com/azharyusof" target="_blank" rel="noopener" class="social-footer-btn" aria-label="GitHub">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="brand-svg"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"></path><path d="M9 18c-4.51 2-5-2-7-2"></path></svg>
        </a>
        <a href="https://linkedin.com" target="_blank" rel="noopener" class="social-footer-btn" aria-label="LinkedIn">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="brand-svg"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect width="4" height="12" x="2" y="9"></rect><circle cx="4" cy="4" r="2"></circle></svg>
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-screen {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem 1.5rem;
  background: var(--bg-app);
}

.back-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  color: var(--text-secondary);
  font-family: var(--font-heading);
  font-weight: 600;
  text-decoration: none;
  margin-bottom: 2rem;
  transition: var(--transition-smooth);
}

.back-link:hover {
  color: var(--accent-color);
  transform: translateX(-3px);
}

.business-card-panel {
  width: 100%;
  max-width: 400px;
  padding: 3rem 2rem 2.5rem;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  box-shadow: var(--shadow-lg);
  border-radius: 1.5rem;
}

.card-profile {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.profile-img {
  width: 110px;
  height: 110px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid var(--bg-app);
  position: relative;
  z-index: 1;
  margin-bottom: 1.25rem;
  box-shadow: var(--shadow-sm);
  transition: var(--transition-smooth);
}

.avatar-glow {
  position: absolute;
  top: -4px;
  width: 118px;
  height: 118px;
  background: var(--gradient-accent);
  border-radius: 50%;
  filter: blur(8px);
  opacity: 0.45;
  animation: pulse-glow 3s ease-in-out infinite;
}

.profile-name {
  font-size: 1.8rem;
  font-weight: 800;
  color: var(--text-primary);
  margin-bottom: 0.25rem;
  line-height: 1.2;
}

.profile-title {
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--accent-color);
}

.profile-company {
  font-size: 0.95rem;
  color: var(--text-secondary);
  margin-bottom: 1rem;
}

.location-badge {
  display: inline-flex;
  align-items: center;
  background: var(--bg-badge);
  color: var(--text-secondary);
  padding: 0.35rem 0.75rem;
  border-radius: 9999px;
  font-size: 0.8rem;
  font-weight: 550;
  border: 1px solid var(--border-color);
}

.icon-spacing {
  margin-right: 0.25rem;
}

.actions-group {
  display: flex;
  flex-direction: column;
  gap: 1.75rem;
}

.save-contact-btn {
  width: 100%;
  justify-content: center;
  font-size: 1.05rem;
  padding: 0.9rem;
}

.save-contact-btn.success {
  background: #10b981;
  box-shadow: 0 4px 14px rgba(16, 185, 129, 0.25);
  border-color: transparent;
}

.communication-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.communication-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  text-decoration: none;
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--text-secondary);
  transition: var(--transition-smooth);
}

.communication-btn:hover {
  color: var(--text-primary);
  transform: translateY(-3px);
}

.comm-icon-box {
  width: 50px;
  height: 50px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  transition: var(--transition-smooth);
}

.communication-btn:hover .comm-icon-box {
  box-shadow: var(--shadow-sm);
  border-color: var(--accent-color);
}

/* Custom platform hover coloring */
.communication-btn:hover .comm-icon-box.call-color {
  color: #3b82f6;
  background: rgba(59, 130, 246, 0.08);
  border-color: rgba(59, 130, 246, 0.3);
}

.communication-btn:hover .comm-icon-box.whatsapp-color {
  color: #10b981;
  background: rgba(16, 185, 129, 0.08);
  border-color: rgba(16, 185, 129, 0.3);
}

.communication-btn:hover .comm-icon-box.email-color {
  color: #ec4899;
  background: rgba(236, 72, 153, 0.08);
  border-color: rgba(236, 72, 153, 0.3);
}

.social-links-footer {
  display: flex;
  justify-content: center;
  gap: 1.25rem;
  border-top: 1px solid var(--border-color);
  padding-top: 1.5rem;
}

.social-footer-btn {
  color: var(--text-secondary);
  transition: var(--transition-smooth);
}

.social-footer-btn:hover {
  color: var(--accent-color);
  transform: translateY(-2px) scale(1.08);
}
</style>
