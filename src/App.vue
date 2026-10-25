<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import '@/index.css'

const skills = [
  { name: 'PROGRAMMING', level: 'Writing clean code in C++, Python, and Java.', category: 'Software', code: 'SYS_01' },
  { name: 'HARDWARE TROUBLESHOOTING', level: 'Testing, diagnostics, and fixing PC/embedded hardware.', category: 'Hardware', code: 'SYS_02' },
  { name: 'PROBLEM SOLVING', level: 'Systematic analysis and logical resolution of tech challenges.', category: 'Systems Logic', code: 'SYS_03' },
  { name: 'EMBEDDED SYSTEMS', level: 'Microcontroller programming (Arduino, ESP32) & Web UI (Vue.js).', category: 'Embedded Dev', code: 'SYS_04' },
]

const projects = [
  {
    number: '01',
    title: 'POWER CONVERSION SYSTEM',
    type: 'ELECTRONICS',
    description: 'Designed, built, and calibrated a power conversion unit supplying regulated DC voltage and current distribution to critical system components.',
    schematic: 'AC/DC Transformer -> Bridge Rectifier -> LM7805 Voltage Regulator -> Output Rail'
  },
  {
    number: '02',
    title: 'AUTOMATED PARKING ENFORCEMENT',
    type: 'MICROPROCESSOR',
    description: 'Smart urban parking solution utilizing Arduino, ultrasonic distance sensors, and a GSM module to detect illegal parking and issue SMS warnings.',
    schematic: 'Ultrasonic Sensor HC-SR04 -> Arduino Uno MCU -> SIM800L GSM Module -> Cellular Alert'
  },
  {
    number: '03',
    title: 'SMART HOME VENTILATION SYSTEM',
    type: 'EMBEDDED SYSTEMS',
    description: 'Cloud-connected thermal monitoring system using ESP32 & DHT sensors to automatically actuate ventilation fans and vent doors based on real-time climate data.',
    schematic: 'DHT22 Sensor -> ESP32 Wi-Fi Node -> Relay Module -> Stepper Motor Vent Door -> Cloud Dashboard'
  },
  {
    number: '04',
    title: 'GOLDEN HARVEST BOARDING FINDER',
    type: 'SOFTWARE DESIGN',
    description: 'Web application designed to help students discover, filter, and navigate suitable boarding houses in Golden Harvest Subdivision.',
    schematic: 'Vue.js Frontend -> REST API Gateway -> SQLite Database -> Interactive Map Integration'
  },
]

// Dropdown state for CV button
const isCvDropdownOpen = ref(false)
const toggleCvDropdown = () => {
  isCvDropdownOpen.value = !isCvDropdownOpen.value
}

// Active Project Schematic Modal
const activeModalProject = ref(null)
const openProjectModal = (project) => {
  activeModalProject.value = project
}
const closeModal = () => {
  activeModalProject.value = null
}

// Close dropdown/modal when clicking outside
const closeDropdown = (e) => {
  if (!e.target.closest('.cv-dropdown-container')) {
    isCvDropdownOpen.value = false
  }
}

// Contact form reactive state
const formName = ref('')
const formEmail = ref('')
const formMessage = ref('')
const isSubmitting = ref(false)
const submitStatus = ref(null) // 'success' | 'error' | null
const statusMessage = ref('')

// Contact form submit handler
const handleSubmit = async () => {
  if (!formName.value.trim() || !formEmail.value.trim() || !formMessage.value.trim()) {
    submitStatus.value = 'error'
    statusMessage.value = '[ERR_01]: All telemetry fields required before transmission.'
    return
  }

  isSubmitting.value = true
  submitStatus.value = null

  try {
    await new Promise((resolve) => setTimeout(resolve, 1200))
    submitStatus.value = 'success'
    statusMessage.value = '[SIGNAL_ACK]: Signal received. Telemetry logged into database.'
    formName.value = ''
    formEmail.value = ''
    formMessage.value = ''
  } catch (err) {
    submitStatus.value = 'error'
    statusMessage.value = '[ERR_02]: Transmission signal lost. Re-attempt signal.'
  } finally {
    isSubmitting.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', closeDropdown)
})

onUnmounted(() => {
  document.removeEventListener('click', closeDropdown)
})
</script>

<template>
  <div class="portfolio-container">
    <!-- Cybernetic Blueprint Grid Overlay -->
    <div class="blueprint-overlay"></div>

    <!-- Glowing Node Pulse Lines -->
    <div class="circuit-pulses">
      <div class="pulse pulse-1"></div>
      <div class="pulse pulse-2"></div>
    </div>

    <!-- Top Blueprint Navigation Header -->
    <header class="navbar">
      <a href="#home" class="brand">
        <div class="brand-chip">CpE</div>
        <div class="brand-name">
          <span>ABEGAIL</span>
          <span class="brand-sub">BALAGON.SYS</span>
        </div>
      </a>

      <nav class="nav-links">
        <a href="#home"><span class="nav-index">01</span> // HOME</a>
        <a href="#about"><span class="nav-index">02</span> // PROFILE</a>
        <a href="#skills"><span class="nav-index">03</span> // MATRIX</a>
        <a href="#projects"><span class="nav-index">04</span> // LOGS</a>
        <a href="#education"><span class="nav-index">05</span> // ACADEMICS</a>
        <a href="#contact" class="nav-cta">TRANSMIT [↗]</a>
      </nav>
    </header>

    <main class="main-content">
      <!-- Hero Section -->
      <section id="home" class="hero-section">
        <div class="hero-copy">
          <div class="sys-badge">
            <span class="sys-dot"></span>
            SYSTEM ONLINE // DISCIPLINE: COMPUTER ENGINEERING
          </div>

          <h1 class="hero-title">
            DESIGN. BUILD.<br />
            <span class="neon-text">INNOVATE.</span>
          </h1>

          <p class="hero-description">
            Hi, I'm <strong class="highlight-text">Abegail Balagon</strong>. I specialize in bridging physical hardware circuits with intelligent software logic — engineering microcontroller systems, hardware diagnostics, and full-stack software interfaces.
          </p>

          <div class="hero-actions">
            <!-- CV Dropdown -->
            <div class="cv-dropdown-container">
              <button @click.stop="toggleCvDropdown" class="btn btn-primary">
                <span>GET RESUME / CV</span>
                <span class="arrow-icon">▼</span>
              </button>

              <div v-if="isCvDropdownOpen" class="cv-dropdown-menu">
                <a href="/Balagon_CV.pdf" target="_blank" class="cv-dropdown-item">
                  <span>VIEW PDF</span> <span>[↗]</span>
                </a>
                <a href="/Balagon_CV.pdf" download="Abegail_Balagon_CV.pdf" class="cv-dropdown-item">
                  <span>DOWNLOAD FILE</span> <span>[↓]</span>
                </a>
              </div>
            </div>

            <a href="#about" class="btn btn-secondary">
              INSPECT SYSTEM SPECS
            </a>
          </div>

          <div class="hero-metrics">
            <div class="metric-card">
              <span class="metric-value">04+</span>
              <span class="metric-label">CORE PROJECTS</span>
            </div>
            <div class="metric-card">
              <span class="metric-value">B.S. CpE</span>
              <span class="metric-label">DEGREE PROGRAM</span>
            </div>
            <div class="metric-card">
              <span class="metric-value">100%</span>
              <span class="metric-label">COMMITMENT</span>
            </div>
          </div>
        </div>

        <!-- Terminal Panel Visual -->
        <div class="hero-visual">
          <div class="terminal-card">
            <div class="terminal-header">
              <div class="terminal-dots">
                <span class="dot red"></span>
                <span class="dot yellow"></span>
                <span class="dot green"></span>
              </div>
              <span class="terminal-title">CPE_DIAGNOSTICS_SHELL v2.6</span>
            </div>
            <div class="terminal-body">
              <p class="term-line"><span class="term-prompt">cpe@system:~$</span> run system_check.sh</p>
              <p class="term-out">[+] Candidate Name: Abegail Balagon</p>
              <p class="term-out">[+] Specialization: Microprocessors &amp; Embedded Systems</p>
              <p class="term-out">[+] Primary Stack: C++, Python, Arduino, Vue.js</p>
              <p class="term-out">[+] Location: Redondo Iguig, Cagayan Valley</p>
              <p class="term-out success">[✓] Hardware Calibration: READY</p>
              <p class="term-out success">[✓] Status: OPEN FOR OJT &amp; COLLABORATION</p>
              <p class="term-line"><span class="term-prompt">cpe@system:~$</span> <span class="blink-cursor">█</span></p>
            </div>
          </div>
        </div>
      </section>

      <!-- Profile Section -->
      <section id="about" class="section-wrap">
        <div class="section-title">
          <span class="section-code">// 01. PROFILE SPECIFICATION</span>
          <h2>ENGINEERING METHODOLOGY</h2>
        </div>

        <div class="about-grid">
          <div class="profile-card">
            <div class="profile-frame">
              <img src="/profile.jpg" alt="Abegail Balagon" class="profile-img" />
              <div class="blueprint-corner top-left"></div>
              <div class="blueprint-corner top-right"></div>
              <div class="blueprint-corner bottom-left"></div>
              <div class="blueprint-corner bottom-right"></div>
            </div>
          </div>

          <div class="about-copy">
            <h3>LOGICAL DESIGN &amp; PRACTICAL HARDWARE</h3>
            <p>
              I am a Computer Engineering student driven by a passion for systematic problem-solving and technical innovation. My expertise covers both hardware design and software architectures.
            </p>
            <p>
              From building power conversion circuits to engineering IoT smart home ventilation systems and microcontroller-based urban enforcement tools, I thrive on turning complex problems into functional real-world systems.
            </p>

            <div class="tech-stack-pills">
              <span class="pill">C++</span>
              <span class="pill">Python</span>
              <span class="pill">Java</span>
              <span class="pill">Arduino</span>
              <span class="pill">ESP32</span>
              <span class="pill">Vue.js</span>
              <span class="pill">Circuit Troubleshooting</span>
            </div>
          </div>
        </div>
      </section>

      <!-- Skills Matrix Section -->
      <section id="skills" class="section-wrap">
        <div class="section-title">
          <span class="section-code">// 02. TECHNICAL MATRIX</span>
          <h2>SKILLS &amp; CAPABILITIES</h2>
        </div>

        <div class="skills-grid">
          <div v-for="skill in skills" :key="skill.name" class="skill-card">
            <div class="skill-top">
              <span class="skill-code">REG: {{ skill.code }}</span>
              <span class="skill-cat">{{ skill.category }}</span>
            </div>
            <h3 class="skill-name">{{ skill.name }}</h3>
            <p class="skill-desc">{{ skill.level }}</p>
            <div class="circuit-bar">
              <div class="circuit-bar-fill"></div>
            </div>
          </div>
        </div>
      </section>

      <!-- Projects Section -->
      <section id="projects" class="section-wrap">
        <div class="section-title">
          <span class="section-code">// 03. SYSTEM LOGS &amp; PROTOTYPES</span>
          <h2>ENGINEERING PROJECTS</h2>
        </div>

        <div class="projects-grid">
          <article v-for="project in projects" :key="project.number" class="project-card">
            <div class="project-top">
              <span class="project-num">LOG #{{ project.number }}</span>
              <span class="project-tag">{{ project.type }}</span>
            </div>

            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>

            <button @click="openProjectModal(project)" class="btn-schematic">
              VIEW SCHEMATIC FLOW ↗
            </button>
          </article>
        </div>
      </section>

      <!-- Academic History Section -->
      <section id="education" class="section-wrap">
        <div class="section-title">
          <span class="section-code">// 04. ACADEMIC RECORD</span>
          <h2>EDUCATION &amp; TIMELINE</h2>
        </div>

        <div class="timeline">
          <div class="timeline-row">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <span class="timeline-year">2019 - PRESENT</span>
              <h3>Bachelor of Science in Computer Engineering</h3>
              <p class="timeline-inst">CAGAYAN STATE UNIVERSITY — Carig Campus</p>
              <span class="badge badge-active">CURRENTLY ENROLLED</span>
            </div>
          </div>

          <div class="timeline-row">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <span class="timeline-year">2017 - 2019</span>
              <h3>Senior High School</h3>
              <p class="timeline-inst">APEC SCHOOLS</p>
              <span class="badge">COMPLETED</span>
            </div>
          </div>

          <div class="timeline-row">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <span class="timeline-year">2013 - 2017</span>
              <h3>Junior High School</h3>
              <p class="timeline-inst">MARIVELES NATIONAL HIGH SCHOOL</p>
              <span class="badge">COMPLETED</span>
            </div>
          </div>

          <div class="timeline-row">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <span class="timeline-year">2006 - 2013</span>
              <h3>Elementary School</h3>
              <p class="timeline-inst">REDONDO ELEMENTARY SCHOOL</p>
              <span class="badge">COMPLETED</span>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact Section -->
      <section id="contact" class="section-wrap">
        <div class="section-title">
          <span class="section-code">// 05. SIGNAL TRANSMISSION</span>
          <h2>CONNECT &amp; COMMUNICATE</h2>
        </div>

        <div class="contact-grid">
          <div class="contact-info-panel">
            <div class="info-card">
              <span class="info-label">EMAIL ADDRESS</span>
              <a href="mailto:balagon.abegail.aura@gmail.com" class="info-val">balagon.abegail.aura@gmail.com</a>
            </div>

            <div class="info-card">
              <span class="info-label">PHONE CONTACT</span>
              <span class="info-val">+63 935 882 4212</span>
            </div>

            <div class="info-card">
              <span class="info-label">LOCATION BASE</span>
              <span class="info-val">Redondo Iguig, Cagayan Valley</span>
            </div>
          </div>

          <div class="contact-form-panel">
            <div class="form-header">TRANSMIT_MESSAGE.EXE</div>
            <form @submit.prevent="handleSubmit" class="telemetry-form">
              <div class="input-group">
                <label for="name">SENDER_NAME</label>
                <input id="name" v-model="formName" type="text" placeholder="Your Name" required />
              </div>

              <div class="input-group">
                <label for="email">SENDER_EMAIL</label>
                <input id="email" v-model="formEmail" type="email" placeholder="email@domain.com" required />
              </div>

              <div class="input-group">
                <label for="message">TRANSMISSION_BODY</label>
                <textarea id="message" v-model="formMessage" rows="4" placeholder="Write message or project proposal..." required></textarea>
              </div>

              <div v-if="submitStatus" :class="['alert-box', submitStatus]">
                {{ statusMessage }}
              </div>

              <button type="submit" class="btn btn-primary btn-full" :disabled="isSubmitting">
                <span v-if="isSubmitting">TRANSMITTING SIGNAL...</span>
                <span v-else>TRANSMIT SIGNAL ↗</span>
              </button>
            </form>
          </div>
        </div>
      </section>
    </main>

    <!-- Schematic Modal -->
    <div v-if="activeModalProject" class="modal-backdrop" @click="closeModal">
      <div class="modal-card" @click.stop>
        <div class="modal-header">
          <span>SCHEMATIC DIAGRAM // LOG #{{ activeModalProject.number }}</span>
          <button @click="closeModal" class="modal-close">✕</button>
        </div>
        <div class="modal-body">
          <h3>{{ activeModalProject.title }}</h3>
          <p class="modal-desc">{{ activeModalProject.description }}</p>
          <div class="schematic-flow">
            <span class="flow-label">SYSTEM DATAFLOW:</span>
            <div class="flow-box">{{ activeModalProject.schematic }}</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Engineering Blueprint Footer -->
    <footer class="footer">
      <div class="footer-inner">
        <div>
          <span class="footer-brand">ABEGAIL BALAGON // B.S. CpE</span>
          <span class="footer-copy">© 2026 ALL RIGHTS RESERVED</span>
        </div>
        <a href="#home" class="back-top">SYSTEM_TOP ↑</a>
      </div>
    </footer>
  </div>
</template>
