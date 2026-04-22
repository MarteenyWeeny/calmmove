<template>
  <div class="modern-portfolio">
    <!-- Animated Mesh Background -->
    <div class="mesh-bg">
      <div class="mesh-circle circle-1"></div>
      <div class="mesh-circle circle-2"></div>
      <div class="mesh-circle circle-3"></div>
      <div class="mesh-circle circle-4"></div>
    </div>

    <nav class="glass-nav">
      <div class="nav-content">
        <div class="logo">it's me</div>
        <div class="links">
          <a href="#projects">PROJECTS</a>
          <a href="#about">ABOUT</a>
          <a href="#contact">CONTACT</a>
        </div>
      </div>
    </nav>

    <main class="main-content">
      <!-- Hero Section -->
      <section class="hero-section">
        <div class="hero-inner">
          <div class="hero-text-block">
            <div class="greeting-bar">
              <span class="emoji">👋</span>
              <span class="greeting">HELLO! I'M JOHN</span>
            </div>
            <h1 class="main-title">
              Crafting <span class="iris-text">Digital</span> <br/>
              Symmetry & <span class="bg-fill">Logic</span>
            </h1>
            <p class="hero-desc">{{ bioExtended }}</p>
            
            <div class="cta-group">
              <button class="magnetic-btn primary">Let's Talk ↗</button>
              <button class="magnetic-btn secondary">Resume ↓</button>
            </div>

            <div class="social-footer">
              <a href="#">FB</a><span>/</span>
              <a href="#">YT</a><span>/</span>
              <a href="#">TW</a>
            </div>
          </div>

          <div class="hero-visual">
            <div class="glass-orb-container">
              <div class="orb-ring ring-1"></div>
              <div class="orb-ring ring-2"></div>
              <div class="img-mask">
                <img :src="profileImage" alt="John Kahano" class="hero-avatar" />
              </div>
              <!-- Floating UI Elements -->
              <div class="float-tag tag-1">Software Designer</div>
              <div class="float-tag tag-2">Nuxt 4 Expert</div>
            </div>
          </div>
        </div>
      </section>

      <!-- Infinit Ticker -->
      <div class="ticker-wrapper">
        <div class="ticker-scroll">
          <span v-for="n in 10" :key="n">DEVELOPMENT ✦ DESIGN ✦ ARCHITECTURE ✦ SYMMETRY ✦ MODERN ✦&nbsp;</span>
        </div>
      </div>

      <!-- Services / Offerings -->
      <section class="services-section" id="about">
        <div class="section-top">
          <span class="sub-label">// CAPABILITIES</span>
          <h2 class="modern-header h-fill">PREMIUM SERVICES</h2>
        </div>

        <div class="services-grid">
          <div class="glass-card service-card reveal-up">
            <div class="card-glow"></div>
            <div class="icon">⚡</div>
            <h3>Full-Stack Dev</h3>
            <p>High-performance logic met with scalable Nuxt 4 architecture.</p>
          </div>
          <div class="glass-card service-card reveal-up" style="animation-delay: 0.1s">
            <div class="card-glow"></div>
            <div class="icon">✨</div>
            <h3>Modern UI/UX</h3>
            <p>Symmetric interfaces focused on modern aesthetics and glassmorphism.</p>
          </div>
          <div class="glass-card service-card reveal-up" style="animation-delay: 0.2s">
            <div class="card-glow"></div>
            <div class="icon">🛠️</div>
            <h3>System Design</h3>
            <p>Strategizing complex digital ecosystems for longevity and speed.</p>
          </div>
        </div>
      </section>

      <!-- Experience Section -->
      <section class="exp-section">
        <div class="glass-card wide-card">
          <h2 class="modern-header">EXPERIENCE</h2>
          <div class="exp-list">
            <div v-for="(edu, index) in education" :key="index" class="exp-row">
              <div class="exp-info">
                <h4>{{ edu.school }}</h4>
                <span>{{ edu.degree }}</span>
              </div>
              <div class="exp-period">2024 - PRESENT</div>
            </div>
            <div v-for="(cert, index) in certifications" :key="'c'+index" class="exp-row">
              <div class="exp-info">
                <h4>{{ cert.name }}</h4>
                <span>{{ cert.issuer }}</span>
              </div>
              <div class="exp-period">{{ cert.date }}</div>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer -->
      <footer class="modern-footer" id="contact">
        <div class="footer-blend">
          <div class="contact-card glass-card">
             <h3>READY TO BUILD?</h3>
             <p class="email-link">{{ email }}</p>
             <div class="footer-socials">
                <a href="#">INSTAGRAM</a>
                <a href="#">DRIBBBLE</a>
                <a href="#">LINKEDIN</a>
             </div>
          </div>
        </div>
        <div class="copyright">© 2026 JOHN KAHANO • BUILT WITH SYMMETRY</div>
      </footer>
    </main>
  </div>
</template>

<script setup>
import { useHead } from '#imports'

const firstName = "John"
const fullName = "John Andrei B. Kahano"
const email = "24-1-02645@vsu.edu.ph"
const bioExtended = "Fusing mathematical logic with avant-garde software design to create immersive, high-performance digital frontiers."
const profileImage = "/kahano.jpg"

useHead({
  title: `${fullName} | Modern Software Designer`,
  meta: [
    { name: 'description', content: `The modern portfolio of ${fullName}.` }
  ]
})

const education = [
  { school: "Visayas State University", degree: "BS Computer Science" }
]

const certifications = [
  { name: "Hackathon 2nd Runner up", issuer: "CSSS", date: "FEB 2026" }
]
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Outfit:wght@400;700;900&display=swap');

.modern-portfolio {
  --bg-color: #fbfbfd;
  --text-primary: #1d1d1f;
  --accent-iris: linear-gradient(135deg, #10b981 0%, #3b82f6 100%);
  --glass-bg: rgba(255, 255, 255, 0.5);
  --glass-border: rgba(255, 255, 255, 0.3);
  
  font-family: 'Plus Jakarta Sans', sans-serif;
  color: var(--text-primary);
  background: var(--bg-color);
  min-height: 100vh;
  overflow-x: hidden;
  position: relative;
}

/* Mesh Background Animation */
.mesh-bg {
  position: fixed;
  top: 0; left: 0; width: 100%; height: 100%;
  z-index: 0;
  overflow: hidden;
  background: #ffffff;
}

.mesh-circle {
  position: absolute;
  filter: blur(140px);
  border-radius: 50%;
  opacity: 0.3;
  animation: meshFloat 20s infinite alternate;
}

.circle-1 { width: 600px; height: 600px; background: #10b981; top: -100px; right: -50px; }
.circle-2 { width: 500px; height: 500px; background: #3b82f6; bottom: -100px; left: -50px; animation-delay: -5s; }
.circle-3 { width: 400px; height: 400px; background: #8b5cf6; top: 30%; left: 10%; animation-delay: -10s; }
.circle-4 { width: 300px; height: 300px; background: #fbbf24; top: 10%; left: 50%; animation-delay: -15s; }

@keyframes meshFloat {
  0% { transform: translate(0, 0) scale(1); }
  50% { transform: translate(10%, 15%) scale(1.1); }
  100% { transform: translate(-5%, -10%) scale(0.9); }
}

/* Glass Nav */
.glass-nav {
  position: fixed;
  top: 20px; left: 50%; transform: translateX(-50%);
  z-index: 1000;
  width: 90%; max-width: 1200px;
  background: var(--glass-bg);
  backdrop-filter: blur(15px);
  border: 1px solid var(--glass-border);
  border-radius: 100px;
  padding: 15px 40px;
}

.nav-content { display: flex; justify-content: space-between; align-items: center; }
.logo { font-family: 'Outfit', sans-serif; font-weight: 800; font-size: 1.2rem; }
.links { display: flex; gap: 30px; font-weight: 700; font-size: 0.8rem; letter-spacing: 1px; }
.links a { text-decoration: none; color: inherit; transition: color 0.3s; }
.links a:hover { color: #10b981; }

.main-content { position: relative; z-index: 10; padding-top: 150px; }

/* Hero Section */
.hero-section { min-height: 80vh; display: flex; align-items: center; padding: 0 5%; margin-bottom: 150px; }
.hero-inner { display: flex; align-items: center; gap: 100px; width: 100%; max-width: 1400px; margin: 0 auto; }

.greeting-bar { 
  background: #1d1d1f; color: white; display: inline-flex; align-items: center; 
  padding: 8px 20px; border-radius: 100px; gap: 10px; margin-bottom: 30px;
  font-weight: 700; font-size: 0.85rem;
}

.main-title { 
  font-family: 'Outfit', sans-serif; font-size: clamp(3rem, 7vw, 5.5rem); 
  font-weight: 900; line-height: 1; letter-spacing: -3px; margin-bottom: 30px; 
}
.iris-text { background: var(--accent-iris); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.bg-fill { -webkit-text-stroke: 2px #1d1d1f; color: transparent; }

.hero-desc { font-size: 1.2rem; color: #6e6e73; max-width: 500px; line-height: 1.6; margin-bottom: 40px; }

.cta-group { display: flex; gap: 20px; margin-bottom: 60px; }
.magnetic-btn { 
  padding: 18px 45px; border-radius: 20px; font-weight: 800; font-size: 1rem; border: none; cursor: pointer;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
.magnetic-btn.primary { background: #1d1d1f; color: white; }
.magnetic-btn.primary:hover { background: #3b82f6; transform: scale(1.05) translateY(-5px); box-shadow: 0 20px 40px rgba(59, 130, 246, 0.2); }
.magnetic-btn.secondary { background: white; border: 1px solid #ddd; }

.social-footer { display: flex; gap: 15px; font-weight: 800; color: #1d1d1f; }
.social-footer a { text-decoration: none; color: inherit; opacity: 0.5; transition: opacity 0.3s; }
.social-footer a:hover { opacity: 1; }

.hero-visual { position: relative; }
.glass-orb-container { position: relative; width: 450px; height: 450px; display: flex; align-items: center; justify-content: center; }

.img-mask { 
  width: 90%; height: 90%; border-radius: 60px; overflow: hidden; background: white;
  border: 1px solid rgba(255,255,255,0.8); box-shadow: 0 100px 150px -50px rgba(0,0,0,0.15);
  position: relative; z-index: 10;
}
.hero-avatar { width: 100%; height: 100%; object-fit: cover; }

.orb-ring { 
  position: absolute; border: 1.5px solid rgba(29,29,31,0.05); border-radius: 50%;
  animation: spin 30s linear infinite;
}
.ring-1 { width: 120%; height: 120%; }
.ring-2 { width: 140%; height: 140%; animation-direction: reverse; animation-duration: 45s; }

.float-tag {
  position: absolute; background: white; border: 1px solid #eee; padding: 12px 25px; border-radius: 20px;
  font-weight: 800; font-size: 0.9rem; z-index: 20; box-shadow: 0 10px 30px rgba(0,0,0,0.05);
  animation: breathe 4s infinite alternate;
}
.tag-1 { top: 10%; right: -20px; }
.tag-2 { bottom: 15%; left: -40px; animation-delay: -2s; }

/* Ticker */
.ticker-wrapper { 
  background: #1d1d1f; color: white; padding: 30px 0; transform: rotate(-1.5deg) scale(1.02);
  margin-bottom: 200px; box-shadow: 0 30px 60px rgba(0,0,0,0.2);
}
.ticker-scroll { display: flex; white-space: nowrap; animation: scrollTicker 30s linear infinite; }
.ticker-scroll span { font-family: 'Outfit', sans-serif; font-weight: 900; font-size: 1.5rem; letter-spacing: 5px; opacity: 0.8; }

/* Glass Cards */
.glass-card {
  background: rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.5);
  border-radius: 40px;
  position: relative;
  overflow: hidden;
  transition: all 0.5s ease;
}

.card-glow {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  background: radial-gradient(circle at center, var(--accent-iris), transparent 70%);
  opacity: 0; transition: opacity 0.5s ease; z-index: -1;
}

.glass-card:hover { 
  transform: translateY(-10px) scale(1.02); 
  border-color: #3b82f6; box-shadow: 0 40px 80px -20px rgba(59, 130, 246, 0.15);
}
.glass-card:hover .card-glow { opacity: 0.05; }

/* Services */
.services-section { padding: 0 5%; margin-bottom: 200px; }
.section-top { text-align: center; margin-bottom: 80px; }
.sub-label { font-weight: 800; font-size: 0.8rem; color: #3b82f6; letter-spacing: 3px; display: block; margin-bottom: 10px; }
.modern-header { font-family: 'Outfit', sans-serif; font-size: 3.5rem; font-weight: 900; letter-spacing: -2px; }
.h-fill { -webkit-text-stroke: 1.5px #1d1d1f; color: transparent; }

.services-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 30px; max-width: 1400px; margin: 0 auto; }
.service-card { padding: 60px 40px; text-align: center; }
.icon { font-size: 3rem; margin-bottom: 30px; }
.service-card h3 { font-size: 1.5rem; font-weight: 800; margin-bottom: 20px; }
.service-card p { color: #6e6e73; line-height: 1.6; }

/* Experience */
.exp-section { padding: 0 5%; margin-bottom: 200px; }
.wide-card { padding: 80px; max-width: 1400px; margin: 0 auto; }
.exp-list { margin-top: 60px; }
.exp-row { display: flex; justify-content: space-between; align-items: center; padding: 40px 0; border-top: 1px solid rgba(0,0,0,0.05); }
.exp-row:last-child { border-bottom: 1px solid rgba(0,0,0,0.05); }
.exp-info h4 { font-size: 1.8rem; font-weight: 800; }
.exp-info span { color: #6e6e73; font-weight: 600; font-size: 1.1rem; }
.exp-period { font-weight: 800; color: #1d1d1f; letter-spacing: 1px; }

/* Footer */
.modern-footer { padding: 200px 5% 50px; background: #1d1d1f; color: white; margin-top: 100px; border-radius: 80px 80px 0 0; }
.contact-card { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.05); padding: 100px; text-align: center; max-width: 1200px; margin: 0 auto 100px; }
.contact-card h3 { font-family: 'Outfit', sans-serif; font-size: clamp(2rem, 5vw, 4rem); font-weight: 900; margin-bottom: 20px; }
.email-link { font-size: clamp(1rem, 2vw, 1.5rem); font-weight: 400; opacity: 0.6; margin-bottom: 60px; }
.footer-socials { display: flex; justify-content: center; gap: 40px; font-weight: 700; font-size: 0.9rem; }
.footer-socials a { color: white; text-decoration: none; opacity: 0.4; transition: opacity 0.3s; }
.footer-socials a:hover { opacity: 1; }

.copyright { text-align: center; font-weight: 800; font-size: 0.75rem; opacity: 0.2; letter-spacing: 2px; }

/* Animations */
@keyframes spin { to { transform: rotate(360deg); } }
@keyframes breathe { from { transform: translateY(0); } to { transform: translateY(-15px); } }
@keyframes scrollTicker { from { transform: translateX(0); } to { transform: translateX(-50%); } }

@media (max-width: 1024px) {
  .hero-inner { flex-direction: column; text-align: center; }
  .main-title { font-size: 4rem; }
  .cta-group { justify-content: center; }
  .services-grid { grid-template-columns: 1fr; }
  .wide-card { padding: 40px 20px; }
  .glass-orb-container { width: 300px; height: 300px; }
  .exp-row { flex-direction: column; align-items: flex-start; gap: 10px; }
  .contact-card { padding: 50px 20px; }
}
</style>