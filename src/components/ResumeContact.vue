<script setup>
import { ref, computed } from 'vue'
import { Mail, Phone, MapPin, Copy, Check, QrCode } from '@lucide/vue'

const email = 'nazhar.myusof@gmail.com'
const phone = '(+60) 19-687 0771'
const location = 'Bandar Puncak Alam, Selangor, Malaysia'

const isCopied = ref(false)

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

// Compute the redirection target URL (VCard contact page)
const targetUrl = computed(() => {
  if (typeof window === 'undefined') return ''
  return window.location.origin + window.location.pathname + '#/contact-card'
})

// Generate custom QR code matching theme styling (Background: card background #131b2e, Foreground: Indigo #6366f1)
const qrCodeUrl = computed(() => {
  if (!targetUrl.value) return ''
  return `https://api.qrserver.com/v1/create-qr-code/?size=180x180&color=6366f1&bgcolor=131b2e&data=${encodeURIComponent(targetUrl.value)}`
})
</script>

<template>
  <section id="contact" class="contact-section">
    <h2 class="section-title">Get In Touch</h2>

    <div class="grid-2 contact-layout">
      <!-- Contact Info Cards -->
      <div class="contact-info">
        <p class="contact-lead">
          I am actively seeking new opportunities and career growth. If you have an open position that matches my skills, feel free to contact me to get in touch.
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

      <!-- Standalone QR Code Redirect Card -->
      <div class="glass-card contact-qr-card">
        <div class="qr-header">
          <QrCode :size="24" class="qr-icon" />
          <h3 class="form-title">Scan Virtual Card</h3>
        </div>
        
        <p class="qr-description">
          Scan the QR code to access my digital profile. Connect instantly via WhatsApp, initiate a direct call, or seamlessly save my contact details to your device.
        </p>

        <div class="qr-display-container">
          <div class="qr-glow-layer"></div>
          <div class="qr-image-wrapper">
            <img :src="qrCodeUrl" alt="Contact QR Code" class="qr-image" />
          </div>
        </div>

        <div class="desktop-fallback">
          <span class="fallback-label">Alternatively, access via direct link:</span>
          <a :href="targetUrl" class="fallback-link">
            azharyusof.github.io/virtual-card
          </a>
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

/* QR Code Card Styles */
.contact-qr-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 1.5rem;
  padding: 2.5rem 2rem;
}

.qr-header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.qr-icon {
  color: var(--accent-color);
}

.form-title {
  font-size: 1.4rem;
  font-weight: 600;
}

.qr-description {
  font-size: 0.95rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

.qr-display-container {
  position: relative;
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0.5rem 0;
}

.qr-glow-layer {
  position: absolute;
  inset: -4px;
  background: var(--gradient-accent);
  border-radius: 1rem;
  filter: blur(10px);
  opacity: 0.35;
}

.qr-image-wrapper {
  position: relative;
  background: #131b2e; /* Mathing --bg-card of dark theme */
  border: 1px solid var(--border-color);
  padding: 0.75rem;
  border-radius: 1rem;
  z-index: 1;
  box-shadow: var(--shadow-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition-smooth);
}

.contact-qr-card:hover .qr-image-wrapper {
  transform: scale(1.04);
  border-color: var(--border-color-hover);
}

.qr-image {
  width: 156px;
  height: 156px;
  display: block;
}

.desktop-fallback {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
  margin-top: 0.5rem;
}

.fallback-label {
  font-size: 0.8rem;
  color: var(--text-muted);
  font-weight: 500;
}

.fallback-link {
  font-family: var(--font-heading);
  font-size: 0.95rem;
  font-weight: 700;
  color: var(--accent-color);
  text-decoration: none;
  transition: var(--transition-smooth);
}

.fallback-link:hover {
  color: var(--text-primary);
  text-decoration: underline;
}

@media print {
  .contact-section {
    padding: 0;
    page-break-inside: avoid;
  }
  .contact-qr-card {
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
