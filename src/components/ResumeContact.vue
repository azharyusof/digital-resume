<script setup>
import { ref } from 'vue'
import { Mail, Phone, MapPin, Copy, Check, Send } from '@lucide/vue'

const email = 'alex.carter@dev.io'
const phone = '+1 (555) 019-2834'
const location = 'San Francisco, CA'

const isCopied = ref(false)
const formSubmitted = ref(false)

const nameInput = ref('')
const emailInput = ref('')
const messageInput = ref('')

const handleCopyEmail = async () => {
  try {
    await navigator.clipboard.writeText(email)
    isCopied.value = true
    setTimeout(() => {
      isCopied.value = false
    }, 2000)
  } catch (err) {
    console.error('Failed to copy text: ', err)
  }
}

const handleSubmit = () => {
  if (!nameInput.value || !emailInput.value || !messageInput.value) return

  // Simulate API post
  formSubmitted.value = true
  
  // Clear form inputs
  nameInput.value = ''
  emailInput.value = ''
  messageInput.value = ''

  setTimeout(() => {
    formSubmitted.value = false
  }, 4000)
}
</script>

<template>
  <section id="contact" class="contact-section">
    <h2 class="section-title">Get In Touch</h2>

    <div class="grid-2 contact-layout">
      <!-- Contact Info Cards -->
      <div class="contact-info">
        <p class="contact-lead">
          I’m always open to discussing new opportunities, freelance projects, or core tech integrations. Drop me a message or copy my email address.
        </p>

        <div class="info-cards-list">
          <!-- Email card with Click to Copy -->
          <div class="glass-card info-card interactive-copy" @click="handleCopyEmail">
            <div class="info-icon-box">
              <Mail :size="20" />
            </div>
            <div class="info-details">
              <span class="info-label">Email</span>
              <span class="info-value">{{ email }}</span>
            </div>
            <button class="copy-btn" :class="{ copied: isCopied }" aria-label="Copy Email">
              <Check v-if="isCopied" :size="16" />
              <Copy v-else :size="16" />
              <span class="copy-tooltip" :class="{ show: isCopied }">Copied!</span>
            </button>
          </div>

          <!-- Phone Card -->
          <div class="glass-card info-card">
            <div class="info-icon-box">
              <Phone :size="20" />
            </div>
            <div class="info-details">
              <span class="info-label">Phone</span>
              <span class="info-value">{{ phone }}</span>
            </div>
          </div>

          <!-- Location Card -->
          <div class="glass-card info-card">
            <div class="info-icon-box">
              <MapPin :size="20" />
            </div>
            <div class="info-details">
              <span class="info-label">Location</span>
              <span class="info-value">{{ location }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Quick Message Form -->
      <div class="glass-card contact-form-card">
        <h3 class="form-title">Send a Message</h3>
        
        <form v-if="!formSubmitted" @submit.prevent="handleSubmit" class="message-form">
          <div class="form-group">
            <label for="name">Your Name</label>
            <input 
              type="text" 
              id="name" 
              v-model="nameInput" 
              placeholder="John Doe" 
              required 
            />
          </div>

          <div class="form-group">
            <label for="email">Email Address</label>
            <input 
              type="email" 
              id="email" 
              v-model="emailInput" 
              placeholder="john@example.com" 
              required 
            />
          </div>

          <div class="form-group">
            <label for="message">Message</label>
            <textarea 
              id="message" 
              v-model="messageInput" 
              rows="4" 
              placeholder="Hi Alex, I'd like to talk about..." 
              required
            ></textarea>
          </div>

          <button type="submit" class="btn btn-primary submit-btn">
            <Send :size="16" /> Send Message
          </button>
        </form>

        <!-- Success Feedback Frame -->
        <div v-else class="success-message animate-fade-in">
          <div class="success-icon-wrapper">
            <Check :size="32" />
          </div>
          <h4>Message Sent!</h4>
          <p>Thank you for reaching out, Alex will get back to you shortly.</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
  padding: 3rem 0 6rem;
}

.contact-layout {
  gap: 3rem;
  margin-top: 1rem;
}

.contact-lead {
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.info-cards-list {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  padding: 1.25rem 1.5rem;
  position: relative;
}

.interactive-copy {
  cursor: pointer;
}

.interactive-copy:hover {
  border-color: var(--accent-color);
  background-color: var(--bg-card-hover);
}

.info-icon-box {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 10px;
  background: var(--bg-badge);
  color: var(--accent-color);
  flex-shrink: 0;
}

.info-details {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
}

.info-label {
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-muted);
}

.info-value {
  font-size: 1rem;
  font-weight: 550;
  color: var(--text-primary);
}

.copy-btn {
  margin-left: auto;
  background: transparent;
  border: none;
  color: var(--text-muted);
  cursor: pointer;
  width: 32px;
  height: 32px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition-smooth);
}

.copy-btn:hover {
  background: var(--bg-badge);
  color: var(--accent-color);
}

.copy-btn.copied {
  color: #10b981;
  background: rgba(16, 185, 129, 0.1);
}

.copy-tooltip {
  position: absolute;
  top: -30px;
  right: 1.5rem;
  background: #10b981;
  color: white;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 600;
  opacity: 0;
  transform: translateY(5px);
  transition: var(--transition-smooth);
  pointer-events: none;
}

.copy-tooltip.show {
  opacity: 1;
  transform: translateY(0);
}

.contact-form-card {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-title {
  font-size: 1.4rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.message-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--text-primary);
}

.form-group input,
.form-group textarea {
  background: rgba(0, 0, 0, 0.15);
  border: 1px solid var(--border-color);
  border-radius: 0.75rem;
  padding: 0.75rem 1rem;
  color: var(--text-primary);
  font-family: var(--font-sans);
  font-size: 0.95rem;
  transition: var(--transition-smooth);
}

.light-mode .form-group input,
.light-mode .form-group textarea {
  background: rgba(255, 255, 255, 0.5);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--accent-color);
  box-shadow: 0 0 0 3px var(--accent-glow);
}

.submit-btn {
  align-self: flex-start;
}

.success-message {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 3rem 1.5rem;
  gap: 1rem;
}

.success-icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 64px;
  height: 64px;
  border-radius: 50%;
  background: rgba(16, 185, 129, 0.15);
  color: #10b981;
  animation: float 4s ease-in-out infinite;
}

.success-message h4 {
  font-size: 1.3rem;
  color: var(--text-primary);
  margin-top: 0.5rem;
}

.success-message p {
  color: var(--text-secondary);
  font-size: 0.95rem;
  max-width: 300px;
}

@media print {
  .contact-section {
    padding: 0;
    page-break-inside: avoid;
  }
  .contact-form-card {
    display: none !important;
  }
  .interactive-copy {
    border: none !important;
    padding: 0.5rem 0 !important;
  }
  .copy-btn {
    display: none !important;
  }
}
</style>
