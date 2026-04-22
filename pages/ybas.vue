<template>
  <div class="space-portfolio">
    <!-- Starfield canvas background -->
    <canvas ref="starCanvas" class="star-canvas"></canvas>

    <div class="app-container">
      <!-- Hero Panel with profile picture -->
      <div class="glass-panel hero-panel">
        <div class="hero-main">
          <!-- Avatar / Profile picture placeholder -->
          <div class="avatar-container">
            <img 
              v-if="profilePicture" 
              :src="profilePicture" 
              alt="Profile"
              class="avatar"
            />
            <div v-else class="avatar-placeholder">
              <i class="fas fa-user-astronaut"></i>
            </div>
            <button class="edit-avatar-btn" @click="triggerFileUpload" title="Change picture">
              <i class="fas fa-camera"></i>
            </button>
            <input 
              type="file" 
              ref="fileInput" 
              style="display: none" 
              accept="image/jpeg,image/png,image/webp"
              @change="onFileSelected"
            />
          </div>

          <div class="hero-info">
            <div class="mission-badge">
              <i class="fas fa-rocket"></i> SPACESHIP LOG // DESIGNATION: CS-EXPLORER
            </div>
            <h1>{{ astronaut.name }}</h1>
            <div class="contact-row">
              <div class="contact-chip"><i class="fas fa-map-marker-alt"></i> Batuan, Bohol · Poblacion Norte</div>
              <div class="contact-chip"><i class="fas fa-envelope"></i> {{ astronaut.email }}</div>
              <div class="contact-chip"><i class="fas fa-phone-alt"></i> {{ astronaut.phone }}</div>
              <div class="contact-chip"><i class="fab fa-github"></i> <a :href="astronaut.github" target="_blank">github.com/MarteenyWeeny</a></div>
            </div>
          </div>
        </div>

        <!-- Streamlined Active Mission Protocol (separate row) -->
        <div class="active-mission-protocol">
          <div class="protocol-track">
            <span class="protocol-led"></span>
            <span class="protocol-label">ACTIVE MISSION PROTOCOL</span>
            <span class="protocol-name">OUTER WILDS · TIMBER HEARTH</span>
          </div>
          <div class="protocol-status">
            <i class="fas fa-satellite-dish"></i> SIGNAL STRONG 
            <span class="status-dots">🟢 🟢 🟢</span>
          </div>
        </div>

        <div class="summary-box">
          <i class="fas fa-quote-left"></i>
          <p>{{ summaryText }}</p>
        </div>
      </div>

      <!-- COMPETITIONS (Mission Logs) -->
      <h2><i class="fas fa-trophy"></i> ✦ MISSION LOGS: COMPETITIONS ✦</h2>
      <div class="comp-grid">
        <div v-for="(comp, idx) in competitions" :key="idx" class="comp-card">
          <span class="rank-badge"><i class="fas fa-award"></i> {{ comp.rank }}</span>
          <div class="comp-title">{{ comp.name }}</div>
          <div class="comp-meta">
            <span><i class="far fa-calendar-alt"></i> {{ comp.date }}</span>
            <span><i class="fas fa-location-dot"></i> {{ comp.location }}</span>
          </div>
          <div class="comp-desc">{{ comp.description }}</div>
        </div>
      </div>

      <!-- Education & Projects -->
      <div class="two-columns">
        <div>
          <h2><i class="fas fa-graduation-cap"></i> ACADEMIC LOG</h2>
          <div class="edu-item">
            <div class="edu-title">
              <span><i class="fas fa-university"></i> Visayas State University</span>
              <span>2024 – 2028</span>
            </div>
            <div>B.S. Computer Science (Expected 2028)</div>
            <div class="coursework">Relevant: Discrete Math, Calculus, Linear Algebra, Computer Programming</div>
          </div>
          <div class="edu-item">
            <div class="edu-title">
              <span><i class="fas fa-atom"></i> Tagbilaran City Science High School</span>
              <span>With Honors</span>
            </div>
            <div>Average Grade: 94.4 · 2018 – 2024</div>
          </div>
        </div>

        <div>
          <h2><i class="fas fa-code-branch"></i> STAR PROJECTS</h2>
          <div class="project-card">
            <div class="project-header">
              <h3><i class="fas fa-utensils"></i> FoodGO</h3>
              <span class="mission-tag">active · sustainability</span>
            </div>
            <p>Surplus food redistribution feature (UI/Frontend/Backend) connecting restaurants with communities to reduce waste.</p>
            <div class="tech-stack">Stack: Vue, Node, Tailwind, Firebase simulation</div>
          </div>
          <div class="project-card quantum-card">
            <i class="fas fa-quantum"></i> <strong>Quantum Computing Exploration</strong>
            <div>QCSP Hackathon 2nd place · Hands-on with Qiskit & quantum gates, solving optimization puzzles.</div>
          </div>
        </div>
      </div>

      <!-- SKILLS -->
      <h2><i class="fas fa-microchip"></i> ✦ PILOT SKILLSET ✦</h2>
      <div class="skills-section">
        <div class="skill-category" v-for="(items, category) in skills" :key="category">
          <h3><i :class="skillIcon(category)"></i> {{ categoryLabel(category) }}</h3>
          <div>
            <span v-for="item in items" class="skill-tag"><i class="fas fa-caret-right"></i> {{ item }}</span>
          </div>
        </div>
      </div>

      <!-- Extra achievements -->
      <div class="extra-panel glass-panel">
        <div><i class="fas fa-shield-haltered"></i> <strong>Capture The Flag (uCTF)</strong> — 10th PH University round · Ethical hacking & cryptography</div>
        <div><i class="fas fa-chalkboard-user"></i> Algolympics 2025 · Top 30 teams (UP-ACM)</div>
        <div class="mission-tag"><i class="fas fa-sync-alt"></i> TIMELOOP READY</div>
      </div>

      <div class="footer-note">
        <i class="fas fa-globe"></i> Outer Wilds protocol · Data core from Martin Benedict Ybas · <i class="fab fa-vuejs"></i> Vue 3 · Deep space exploration<br/>
        ✦ "The universe is, and we are." – ready for new orbits ✦
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// ---------- DATA ----------
const astronaut = ref({
  name: "Martin Benedict E. Ybas",
  email: "24-1-01033@vsu.edu.ph",
  phone: "+63 916 255 5259",
  github: "https://github.com/MarteenyWeeny"
})

const summaryText = ref("Motivated Computer Science student with a strong foundation in competitive programming, algorithm design, and hackathons. Experienced in C/C++, Java, Python, CTF events, and quantum computing. Passionate about open-source, logic puzzles, and exploring the cosmos of code.")

const competitions = ref([
  { name: "QCSP Quantum Computing Hackathon", rank: "2nd place", date: "October 2024", location: "UP Tacloban (On site)", description: "Hands-on quantum algorithms (Qiskit) solving advanced optimization problems." },
  { name: "CS Week · C/C++/Java Programming Competition", rank: "3rd place", date: "February 2025", location: "VSU", description: "Efficient algorithms under time pressure, top 3 department." },
  { name: "CS Week · Hackathon", rank: "3rd place", date: "February 2025", location: "VSU", description: "Team-based creative solutions for real-world challenges." },
  { name: "UP-ACM Algolympics", rank: "Top 30 teams", date: "March 2025", location: "Online", description: "Complex problem-solving with innovative strategies." },
  { name: "RSCENE Code-It Programming Competition", rank: "3rd place", date: "June 2025", location: "Catbalogan City", description: "Optimized code balancing complexity and runtime." },
  { name: "Trend Micro uCTF", rank: "10th place", date: "August 2025", location: "Online", description: "Security, cryptography, ethical hacking in CTF." },
  { name: "CS Week · C/C++/Java Programming Competition", rank: "1st place", date: "March 2026", location: "VSU", description: "Refined algorithm design, superior problem-solving." }
])

const skills = ref({
  languages: ["C", "C++", "Java", "Python", "JavaScript", "HTML/CSS"],
  tools: ["Git", "Linux", "Visual Studio Code", "LaTeX", "GCC/G++"],
  technical: ["Algorithm Design", "Data Structures", "OOP", "Problem Solving", "Basic Quantum Algorithms"],
  interests: ["Competitive Programming", "Open Source", "Hackathons", "Logic Puzzles", "Academic Writing", "Math Olympiads"]
})

// Profile picture handling
const profilePicture = ref('/ybas.png')
const fileInput = ref(null)

const triggerFileUpload = () => {
  fileInput.value.click()
}

const onFileSelected = (event) => {
  const file = event.target.files[0]
  if (file && (file.type === 'image/jpeg' || file.type === 'image/png' || file.type === 'image/webp')) {
    const reader = new FileReader()
    reader.onload = (e) => {
      profilePicture.value = e.target.result
    }
    reader.readAsDataURL(file)
  } else {
    alert("Please select a JPG, PNG, or WEBP image.")
  }
}

// Helper methods
const skillIcon = (category) => {
  const icons = {
    languages: "fas fa-code",
    tools: "fas fa-wrench",
    technical: "fas fa-brain",
    interests: "fas fa-heart"
  }
  return icons[category] || "fas fa-star"
}
const categoryLabel = (category) => {
  const labels = {
    languages: "Languages",
    tools: "Tools & OS",
    technical: "Technical",
    interests: "Interests"
  }
  return labels[category] || category
}

// ---------- STARFIELD CANVAS ----------
const starCanvas = ref(null)
let animationId = null
let stars = []

const initStars = () => {
  const canvas = starCanvas.value
  if (!canvas) return
  const w = window.innerWidth
  const h = window.innerHeight
  canvas.width = w
  canvas.height = h
  const starCount = 400
  stars = []
  for (let i = 0; i < starCount; i++) {
    stars.push({
      x: Math.random() * w,
      y: Math.random() * h,
      radius: Math.random() * 1.8,
      alpha: Math.random() * 0.5 + 0.3,
      speed: 0.002 + Math.random() * 0.01,
      twinkle: Math.random() * Math.PI * 2
    })
  }
}

const drawStars = () => {
  const canvas = starCanvas.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')
  const w = window.innerWidth
  const h = window.innerHeight
  if (canvas.width !== w || canvas.height !== h) {
    canvas.width = w
    canvas.height = h
    initStars()
  }
  ctx.clearRect(0, 0, w, h)
  const grad = ctx.createLinearGradient(0, 0, w*0.3, h*0.5)
  grad.addColorStop(0, '#03040b')
  grad.addColorStop(1, '#010101')
  ctx.fillStyle = grad
  ctx.fillRect(0, 0, w, h)
  
  for (let s of stars) {
    const twinkleVal = 0.4 + 0.5 * Math.sin(Date.now() * s.speed + s.twinkle)
    let alphaVal = Math.min(0.9, Math.max(0.2, s.alpha * twinkleVal))
    ctx.beginPath()
    ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2)
    ctx.fillStyle = `rgba(255, 220, 170, ${alphaVal})`
    ctx.fill()
    if (alphaVal > 0.7) {
      ctx.beginPath()
      ctx.arc(s.x, s.y, s.radius * 1.7, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(255, 180, 80, 0.1)`
      ctx.fill()
    }
  }
  animationId = requestAnimationFrame(drawStars)
}

const handleResize = () => {
  initStars()
}

onMounted(() => {
  initStars()
  drawStars()
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  if (animationId) cancelAnimationFrame(animationId)
  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.space-portfolio {
  background-color: #03050b;
  font-family: 'Space Grotesk', 'Segoe UI', system-ui, sans-serif;
  color: #eef4ff;
  line-height: 1.5;
  min-height: 100vh;
  position: relative;
}

.star-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.app-container {
  position: relative;
  z-index: 2;
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem 1.5rem 4rem;
}

.glass-panel {
  background: rgba(8, 12, 25, 0.65);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(88, 130, 193, 0.3);
  border-radius: 2rem;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(70, 130, 200, 0.2) inset;
  transition: transform 0.2s, border-color 0.2s;
}
.glass-panel:hover {
  border-color: rgba(255, 140, 50, 0.5);
}

.hero-panel {
  padding: 1.8rem;
  margin-bottom: 2rem;
}

/* Hero main row: avatar + info */
.hero-main {
  display: flex;
  flex-wrap: wrap;
  gap: 1.8rem;
  align-items: center;
  margin-bottom: 1.5rem;
}

.avatar-container {
  position: relative;
  flex-shrink: 0;
}
.avatar, .avatar-placeholder {
  width: 110px;
  height: 110px;
  border-radius: 50%;
  object-fit: cover;
  background: #1f2b48;
  border: 3px solid #f97316;
  box-shadow: 0 0 15px rgba(249, 115, 22, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
  color: #f97316;
}
.edit-avatar-btn {
  position: absolute;
  bottom: 5px;
  right: 5px;
  background: #0f1425;
  border: 1px solid #f97316;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #f97316;
  transition: 0.2s;
}
.edit-avatar-btn:hover {
  background: #f97316;
  color: #03050b;
}

.hero-info {
  flex: 1;
}
.mission-badge {
  font-family: 'Share Tech Mono', monospace;
  font-size: 0.8rem;
  background: #f9731622;
  padding: 0.2rem 0.8rem;
  border-radius: 30px;
  display: inline-block;
  border: 1px solid #f9731655;
}
h1 {
  font-size: 2.7rem;
  font-weight: 700;
  margin: 0.5rem 0 0.2rem;
}

.contact-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
  margin-top: 0.6rem;
}
.contact-chip {
  background: #0f1425cc;
  border-radius: 60px;
  padding: 0.3rem 1rem;
  font-size: 0.85rem;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  border: 1px solid #2a3b5c;
}
.contact-chip a {
  color: #eef4ff;
  text-decoration: none;
}
.contact-chip:hover {
  border-color: #f97316;
}

/* Streamlined Active Mission Protocol */
.active-mission-protocol {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
  border-radius: 60px;
  padding: 0.6rem 1.2rem;
  margin: 1rem 0 1.2rem;
  border: 1px solid rgba(249, 115, 22, 0.4);
}
.protocol-track {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  font-family: 'Share Tech Mono', monospace;
  font-size: 0.8rem;
}
.protocol-led {
  width: 10px;
  height: 10px;
  background-color: #f97316;
  border-radius: 50%;
  box-shadow: 0 0 6px #f97316;
  animation: pulse 1.2s infinite;
}
.protocol-label {
  letter-spacing: 1px;
  font-weight: 600;
}
.protocol-name {
  color: #f97316;
  font-weight: bold;
}
.protocol-status {
  font-size: 0.75rem;
  display: flex;
  align-items: center;
  gap: 0.4rem;
}
.status-dots {
  letter-spacing: 2px;
}

@keyframes pulse {
  0% { opacity: 0.4; transform: scale(0.8);}
  100% { opacity: 1; transform: scale(1.2);}
}

.summary-box {
  background: #0a0f1f60;
  border-radius: 1.5rem;
  padding: 1rem;
  display: flex;
  gap: 0.8rem;
  align-items: flex-start;
  margin-top: 0.5rem;
}
.summary-box i {
  color: #f97316;
  font-size: 1.2rem;
}

/* rest of styles (unchanged, kept from previous) */
h2 {
  font-size: 1.8rem;
  margin: 2rem 0 1.5rem;
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  border-left: 4px solid #f97316;
  padding-left: 1rem;
  font-family: 'Share Tech Mono', monospace;
  text-transform: uppercase;
}
h2 i { color: #f97316; }

.comp-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(330px, 1fr));
  gap: 1.5rem;
  margin-bottom: 1rem;
}
.comp-card {
  background: rgba(5, 8, 18, 0.7);
  backdrop-filter: blur(8px);
  border-radius: 1.5rem;
  padding: 1.2rem;
  border-left: 4px solid #f97316;
  transition: transform 0.2s;
}
.comp-card:hover { transform: translateY(-5px); box-shadow: 0 20px 30px -12px black; }
.rank-badge {
  background: #f97316;
  color: #03050b;
  font-weight: bold;
  font-size: 0.7rem;
  padding: 0.2rem 0.7rem;
  border-radius: 30px;
}
.comp-title { font-size: 1.2rem; font-weight: 600; margin: 0.5rem 0 0.3rem; }
.comp-meta { font-size: 0.75rem; font-family: monospace; color: #9ab3d5; display: flex; gap: 1rem; flex-wrap: wrap; }
.comp-desc { font-size: 0.85rem; color: #cdddf9; margin-top: 0.6rem; }

.two-columns {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
  margin: 1rem 0;
}
.edu-item, .project-card {
  background: rgba(12, 18, 34, 0.7);
  backdrop-filter: blur(8px);
  border-radius: 1.2rem;
  padding: 1.2rem;
  margin-bottom: 1rem;
  border: 1px solid #2c3e5e;
}
.edu-title { display: flex; justify-content: space-between; flex-wrap: wrap; font-weight: 700; margin-bottom: 0.3rem; }
.coursework { font-size: 0.8rem; margin-top: 0.4rem; color: #bdd4ff; }
.project-header { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; }
.quantum-card { border-left: 3px solid #3b82f6; }
.tech-stack { font-size: 0.75rem; margin-top: 0.5rem; font-family: monospace; }

.skills-section {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin: 1.5rem 0;
}
.skill-category {
  flex: 1;
  min-width: 180px;
  background: rgba(0,0,0,0.4);
  border-radius: 1.2rem;
  padding: 1rem;
}
.skill-category h3 { font-size: 1rem; margin-bottom: 0.6rem; border-bottom: 1px dashed #f97316; display: inline-block; }
.skill-tag {
  display: inline-block;
  background: #1f2b48;
  padding: 0.2rem 0.9rem;
  border-radius: 30px;
  font-size: 0.75rem;
  margin: 0.3rem 0.3rem;
  font-family: monospace;
  border: 1px solid #3e5a7c;
}
.extra-panel {
  margin-top: 2rem;
  padding: 1rem 1.5rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}
.mission-tag {
  background: #f9731622;
  padding: 0.2rem 0.8rem;
  border-radius: 40px;
  font-size: 0.7rem;
  font-family: monospace;
}
.footer-note {
  text-align: center;
  margin-top: 3rem;
  font-size: 0.75rem;
  color: #7e95b9;
  border-top: 1px dashed #2c3e5e;
  padding-top: 2rem;
}
@media (max-width: 780px) {
  .app-container { padding: 1rem; }
  h2 { font-size: 1.4rem; }
  h1 { font-size: 2rem; }
  .avatar, .avatar-placeholder { width: 70px; height: 70px; font-size: 2rem; }
  .hero-main { gap: 1rem; }
}
</style>