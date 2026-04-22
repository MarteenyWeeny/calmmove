<template>
  <div class="page">

    <!-- Animated background canvas -->
    <canvas ref="bgCanvas" class="bg-canvas"></canvas>
    <div class="bg-vignette"></div>
    <div class="grain"></div>

    <!-- Ember particles -->
    <div class="embers" ref="embersWrap"></div>

    <div class="page-inner">

      <!-- Top Rule -->
      <div class="top-rule">
        <div class="rule-line"></div>
        <span class="rule-cross">✝</span>
        <span class="rule-label">CS Student · Web Dev · Builder</span>
        <span class="rule-cross">✝</span>
        <div class="rule-line"></div>
      </div>

      <!-- Hero -->
      <header class="hero">
        <div class="hero-left">
          <div class="av-frame">
            <div class="av-border"></div>
            <div class="av-corner tl"></div>
            <div class="av-corner tr"></div>
            <div class="av-corner bl"></div>
            <div class="av-corner br"></div>
            <div class="av-inner">
              <img v-if="profileImage" :src="profileImage" :alt="fullName" class="av-img" />
              <svg v-else class="av-svg" viewBox="0 0 124 144" xmlns="http://www.w3.org/2000/svg">
                <rect width="124" height="144" fill="#0f0b08"/>
                <line x1="0" y1="28" x2="124" y2="28" stroke="rgba(139,26,26,.12)" stroke-width=".5"/>
                <line x1="0" y1="48" x2="124" y2="48" stroke="rgba(139,26,26,.12)" stroke-width=".5"/>
                <line x1="0" y1="68" x2="124" y2="68" stroke="rgba(139,26,26,.12)" stroke-width=".5"/>
                <line x1="0" y1="88" x2="124" y2="88" stroke="rgba(139,26,26,.12)" stroke-width=".5"/>
                <line x1="0" y1="108" x2="124" y2="108" stroke="rgba(139,26,26,.12)" stroke-width=".5"/>
                <line x1="0" y1="128" x2="124" y2="128" stroke="rgba(139,26,26,.12)" stroke-width=".5"/>
                <line x1="62" y1="10" x2="62" y2="134" stroke="rgba(139,26,26,.3)" stroke-width="1"/>
                <line x1="20" y1="56" x2="104" y2="56" stroke="rgba(139,26,26,.3)" stroke-width="1"/>
                <circle cx="62" cy="56" r="28" fill="rgba(139,26,26,.06)"/>
                <text x="62" y="44" font-family="Cinzel, serif" font-size="13" font-weight="400"
                  fill="rgba(212,196,168,.5)" text-anchor="middle" letter-spacing="3">{{ initials.first }}</text>
                <text x="62" y="72" font-family="Cinzel, serif" font-size="26" font-weight="700"
                  fill="#d4c4a8" text-anchor="middle" letter-spacing="2">{{ initials.mono }}</text>
                <rect x="6" y="6" width="10" height="10" fill="none" stroke="rgba(201,168,76,.35)" stroke-width="1"/>
                <rect x="108" y="6" width="10" height="10" fill="none" stroke="rgba(201,168,76,.35)" stroke-width="1"/>
                <rect x="6" y="128" width="10" height="10" fill="none" stroke="rgba(201,168,76,.35)" stroke-width="1"/>
                <rect x="108" y="128" width="10" height="10" fill="none" stroke="rgba(201,168,76,.35)" stroke-width="1"/>
              </svg>
            </div>
          </div>
          <div class="av-tag">
            <span class="av-tag-cross">✝</span>
            <span class="av-tag-text">Genei Ryodan</span>
          </div>
        </div>

        <div class="hero-text">
          <div class="h-label">
            <span class="h-label-cross">✝</span>
            CS Student · Web Dev · Builder
            <span class="h-label-cross">✝</span>
          </div>

          <h1 class="hero-name">
            <span class="fn">{{ nameParts.first }}</span>
            <span class="ln">{{ nameParts.last }}</span>
          </h1>

          <a :href="`mailto:${email}`" class="hero-email">
            <span class="hero-email-glyph">✉</span>
            {{ email }}
          </a>

          <p class="hero-bio">{{ bio }}</p>
        </div>
      </header>

      <!-- Content Grid -->
      <main class="content-grid">
        <div class="col">

          <!-- Skills -->
          <div class="card">
            <div class="cc tl"></div><div class="cc tr"></div>
            <div class="cc bl"></div><div class="cc br"></div>
            <div class="card-title"><span class="ct-num">I.</span> Abilities Stolen</div>
            <div class="sdiv"><div class="sdiv-line"></div><span class="sdiv-glyph">✦</span></div>
            <div class="skills">
              <div
                v-for="(skill, i) in skills"
                :key="i"
                class="s-tag"
                :style="`animation-delay: ${0.4 + i * 0.12}s`"
              >
                <span class="s-dot"></span>{{ skill }}
              </div>
            </div>
          </div>

          <!-- Certs -->
          <div class="card">
            <div class="cc tl"></div><div class="cc tr"></div>
            <div class="cc bl"></div><div class="cc br"></div>
            <div class="card-title"><span class="ct-num">III.</span> Seals &amp; Marks</div>
            <div class="sdiv"><div class="sdiv-line"></div><span class="sdiv-glyph">✦</span></div>
            <div v-for="(cert, i) in certifications" :key="i" class="cert">
              <div class="cert-seal">✝</div>
              <div>
                <p class="cert-name">{{ cert.name }}</p>
                <p class="cert-org">{{ cert.issuer }}</p>
                <p class="cert-date">{{ cert.date }}</p>
              </div>
            </div>
          </div>

        </div>
        <div class="col">

          <!-- Education -->
          <div class="card">
            <div class="cc tl"></div><div class="cc tr"></div>
            <div class="cc bl"></div><div class="cc br"></div>
            <div class="card-title"><span class="ct-num">II.</span> Chronicle of Learning</div>
            <div class="sdiv"><div class="sdiv-line"></div><span class="sdiv-glyph">✦</span></div>
            <div v-for="(edu, i) in education" :key="i" class="edu">
              <div class="edu-spine">
                <div class="edu-rune">✦</div>
                <div class="edu-vline"></div>
              </div>
              <div>
                <h3 class="edu-school">{{ edu.school }}</h3>
                <p class="edu-deg">{{ edu.degree }}</p>
                <span class="edu-dates">{{ edu.dates }}</span>
              </div>
            </div>
          </div>

          <!-- Projects -->
          <div class="card">
            <div class="cc tl"></div><div class="cc tr"></div>
            <div class="cc bl"></div><div class="cc br"></div>
            <div class="card-title"><span class="ct-num">IV.</span> The Book of Works</div>
            <div class="sdiv"><div class="sdiv-line"></div><span class="sdiv-glyph">✦</span></div>
            <div v-for="(project, i) in projects" :key="i" class="project">
              <div class="proj-head">
                <h3 class="proj-name">{{ project.name }}</h3>
                <span class="proj-dates">{{ project.dates }}</span>
              </div>
              <p class="proj-desc">{{ project.description }}</p>
              <div class="proj-status">
                <span class="proj-status-label">In Progress</span>
                <div class="proj-bar"><div class="proj-bar-fill"></div></div>
              </div>
            </div>
          </div>

        </div>
      </main>

      <!-- Footer -->
      <div class="footer">
        <div class="footer-orn">
          <div class="footer-line"></div>
          <span class="footer-cross">✝</span>
          <div class="footer-line"></div>
        </div>
        <p class="footer-text">{{ fullName }} · Built with curiosity &amp; code</p>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useHead } from '#imports'

// ==========================================
// MEMBER CONFIGURATION: Edit details below
// ==========================================

const fullName = "Radz Ponce A. Moreno"
const email = "24-1-01485@vsu.edu.ph"
const bio = "I build software that turns ideas into impact. As a Computer Science student, I focus on web development, algorithms, and system design to create fast, clean, and reliable digital experiences. I’m driven by curiosity, obsessed with improvement, and motivated to ship technology that solves real problems."
const profileImage = "/rmoreno.jpg" // Image must be inside public/ directory

useHead({
  title: fullName,
  meta: [{ name: 'description', content: `The personal page of ${fullName}.` }],
  bodyAttrs: {
    class: 'rmoreno-theme'
  }
})

const education = [
  {
    school: "Visayas State University",
    degree: "Bachelor of Science in Computer Science",
    dates: "August 2024 – Present"
  }
]

const projects = [
  {
    name: "LetMCook",
    dates: "March 2026 – Present",
    description: "Smart meal planner using your ingredients to meet nutrient goals — a stolen technique, perfected."
  }
]

const certifications = [
  {
    name: "Problem Solving Certificate",
    issuer: "HackerRank",
    date: "August 2025"
  }
]

const skills = ["C / C++", "TypeScript", "Python", "Java"]

// ── Derived ──
const nameParts = computed(() => {
  const parts = fullName.trim().split(' ')
  const last  = parts.pop()
  return { first: parts.join(' '), last }
})

const initials = computed(() => {
  const words = fullName.trim().split(' ')
  return {
    first: words[0]?.toUpperCase() ?? '',
    mono:  (words[0]?.[0] ?? '') + (words[words.length - 1]?.[0] ?? '')
  }
})

// ── Canvas orbs ──
const bgCanvas = ref(null)

onMounted(() => {
  // Ember particles
  const wrap = document.querySelector('.embers')
  for (let i = 0; i < 22; i++) {
    const e = document.createElement('div')
    e.className = 'ember'
    const sz = Math.random() * 3 + 1
    e.style.cssText = `
      left: ${Math.random() * 100}%;
      width: ${sz}px; height: ${sz}px;
      animation-duration: ${Math.random() * 5 + 3}s;
      animation-delay: ${Math.random() * 7}s;
      --dx: ${(Math.random() - .5) * 80}px;
    `
    wrap.appendChild(e)
  }

  // Canvas
  const cv = bgCanvas.value
  const cx = cv.getContext('2d')
  function rsz() { cv.width = window.innerWidth; cv.height = window.innerHeight }
  rsz()
  window.addEventListener('resize', rsz)

  const orbs = [
    { x: window.innerWidth * .2, y: window.innerHeight * .2, r: 260, vx: .15, vy: .10, c: '139,26,26' },
    { x: window.innerWidth * .8, y: window.innerHeight * .7, r: 200, vx: -.10, vy: .14, c: '80,10,10' },
    { x: window.innerWidth * .5, y: window.innerHeight * .9, r: 180, vx: .08, vy: -.12, c: '60,15,5' },
  ];

  (function loop() {
    cx.clearRect(0, 0, cv.width, cv.height)
    orbs.forEach(o => {
      o.x += o.vx; o.y += o.vy
      if (o.x < -o.r) o.x = cv.width + o.r
      if (o.x > cv.width + o.r) o.x = -o.r
      if (o.y < -o.r) o.y = cv.height + o.r
      if (o.y > cv.height + o.r) o.y = -o.r
      const g = cx.createRadialGradient(o.x, o.y, 0, o.x, o.y, o.r)
      g.addColorStop(0, `rgba(${o.c},.13)`)
      g.addColorStop(1, `rgba(${o.c},0)`)
      cx.fillStyle = g
      cx.beginPath(); cx.arc(o.x, o.y, o.r, 0, Math.PI * 2); cx.fill()
    })
    requestAnimationFrame(loop)
  })()
})
</script>

<style>
body.rmoreno-theme {
  background-color: #0d0a07;
  color: #e0d0b0;
}
</style>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=IM+Fell+English:ital@0;1&family=Cinzel:wght@400;600;700;900&family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap');

/* ── Variables ── */
:root {
  --blood:    #a82020;
  --crimson:  #c0392b;
  --gold:     #d4aa50;
  --gold-dim: #b8922a;
  --ink:      #0d0a07;
  --ash:      #1a1208;
  --smoke:    #9a8470;
  --bone:     #e0d0b0;
  --ghost:    #b8a890;
  --white:    #f8f0e0;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

/* ── Page shell ── */
.page {
  position: relative;
  min-height: 100vh;
  background-color: var(--ink);
  color: var(--bone);
  font-family: 'Crimson Pro', Georgia, serif;
  overflow-x: hidden;
  cursor: crosshair;
}

/* ── Background layers ── */
.bg-canvas {
  position: fixed; inset: 0;
  width: 100%; height: 100%;
  pointer-events: none; z-index: 0;
}
.bg-vignette {
  position: fixed; inset: 0; z-index: 0;
  background: radial-gradient(ellipse 80% 80% at 50% 50%, transparent 40%, rgba(0,0,0,.7) 100%);
  pointer-events: none;
}
.grain {
  position: fixed; inset: -200%;
  width: 400%; height: 400%;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  opacity: .04;
  pointer-events: none; z-index: 0;
  animation: grain .12s steps(1) infinite;
}
@keyframes grain {
  0%  { transform: translate(0,0) }
  25% { transform: translate(-4%,-4%) }
  50% { transform: translate(4%,0) }
  75% { transform: translate(0,4%) }
}

/* ── Embers ── */
.embers {
  position: fixed; bottom: 0; left: 0; right: 0;
  pointer-events: none; z-index: 0; height: 220px; overflow: hidden;
}
.ember {
  position: absolute; bottom: 0; border-radius: 50%;
  background: radial-gradient(circle, #ffd070 0%, #c0392b 50%, transparent 100%);
  opacity: 0;
  animation: emberRise linear infinite;
}
@keyframes emberRise {
  0%   { transform: translateY(0) translateX(0) scale(1); opacity: .75; }
  70%  { opacity: .3; }
  100% { transform: translateY(-200px) translateX(var(--dx)) scale(.1); opacity: 0; }
}

/* ── Inner wrapper ── */
.page-inner {
  position: relative; z-index: 1;
  max-width: 1000px; margin: 0 auto;
  padding: 56px 32px 90px;
  background: rgba(13,10,7,0.5);
}

/* ── Top rule ── */
.top-rule {
  display: flex; align-items: center; gap: 16px;
  margin-bottom: 52px;
  opacity: 0; animation: rise .8s ease forwards .1s;
}
.rule-line {
  flex: 1; height: 1px;
  background: linear-gradient(to right, transparent, rgba(212,170,80,.5), transparent);
}
.rule-cross {
  color: var(--gold); font-size: 1rem;
  text-shadow: 0 0 14px rgba(212,170,80,.7);
  animation: candleGlow 3s ease-in-out infinite;
}
.rule-label {
  font-family: 'Cinzel', serif; font-size: .5rem;
  letter-spacing: .32em; color: var(--gold); text-transform: uppercase;
}
@keyframes candleGlow {
  0%,100% { text-shadow: 0 0 8px rgba(212,170,80,.5); opacity: .85; }
  50%      { text-shadow: 0 0 22px rgba(212,170,80,1), 0 0 44px rgba(212,170,80,.3); opacity: 1; }
}

/* ── Hero ── */
.hero {
  display: grid;
  grid-template-columns: 150px 1fr;
  gap: 52px; align-items: start;
  margin-bottom: 60px;
}
.hero-left { display: flex; flex-direction: column; align-items: center; gap: 14px; }

/* Avatar frame */
.av-frame { position: relative; width: 140px; height: 160px; }
.av-border {
  position: absolute; inset: 0;
  border: 1px solid rgba(212,170,80,.35);
  box-shadow: inset 0 0 30px rgba(168,32,32,.3), 0 0 25px rgba(0,0,0,.8);
}
.av-border::before {
  content: '';
  position: absolute; inset: 5px;
  border: 1px solid rgba(168,32,32,.2);
}
.av-corner {
  position: absolute; width: 12px; height: 12px;
  border-color: var(--gold); border-style: solid;
}
.av-corner.tl { top: -1px; left: -1px;   border-width: 2px 0 0 2px; }
.av-corner.tr { top: -1px; right: -1px;  border-width: 2px 2px 0 0; }
.av-corner.bl { bottom: -1px; left: -1px; border-width: 0 0 2px 2px; }
.av-corner.br { bottom: -1px; right: -1px;border-width: 0 2px 2px 0; }

.av-inner {
  position: absolute; inset: 8px;
  background: #0f0b08; overflow: hidden;
  display: flex; align-items: center; justify-content: center;
}
.av-img { width: 100%; height: 100%; object-fit: cover; }
.av-svg { width: 100%; height: 100%; }

/* Sigil tag */
.av-tag { display: flex; flex-direction: column; align-items: center; gap: 4px; }
.av-tag-cross {
  font-size: 1.6rem; color: var(--blood); line-height: 1;
  text-shadow: 0 0 14px rgba(168,32,32,.9);
  animation: candleGlow 4s ease-in-out infinite;
}
.av-tag-text {
  font-family: 'Cinzel', serif; font-size: .44rem;
  letter-spacing: .26em; text-transform: uppercase; color: var(--gold);
}

/* Hero text */
.hero-text { padding-top: 4px; }

.h-label {
  display: flex; align-items: center; gap: 10px;
  font-family: 'Cinzel', serif; font-size: .56rem;
  letter-spacing: .2em; color: #d45a5a;
  text-transform: uppercase; margin-bottom: 16px;
  opacity: 0; animation: rise .6s ease forwards .2s;
}
.h-label-cross { color: #d45a5a; font-size: .85rem; text-shadow: 0 0 8px rgba(212,90,90,.8); }

.hero-name {
  font-family: 'Cinzel', serif; font-weight: 900;
  line-height: .92; margin-bottom: 20px;
  opacity: 0; animation: rise .7s ease forwards .35s;
}
.hero-name .fn {
  display: block;
  font-size: clamp(1.5rem, 3vw, 2.2rem);
  color: var(--bone); letter-spacing: .05em;
}
.hero-name .ln {
  display: block;
  font-size: clamp(2.2rem, 5vw, 3.6rem);
  color: var(--white); letter-spacing: .07em;
  text-shadow: 0 2px 24px rgba(168,32,32,.4);
  position: relative;
}
.hero-name .ln::after {
  content: '';
  position: absolute; bottom: -8px; left: 0;
  width: 55%; height: 1px;
  background: linear-gradient(to right, var(--blood), transparent);
}

.hero-email {
  display: inline-flex; align-items: center; gap: 8px;
  font-family: 'IM Fell English', serif; font-style: italic;
  font-size: .98rem; color: var(--ghost);
  text-decoration: none; margin: 20px 0 22px;
  transition: color .3s;
  opacity: 0; animation: rise .6s ease forwards .5s;
}
.hero-email:hover { color: var(--gold); }
.hero-email-glyph { color: var(--blood); }

.hero-bio {
  font-family: 'IM Fell English', serif;
  font-size: 1.05rem; line-height: 1.8; font-style: italic;
  color: var(--ghost); max-width: 530px;
  border-left: 2px solid var(--blood);
  padding-left: 18px;
  opacity: 0; animation: rise .6s ease forwards .65s;
}

@keyframes rise {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ── Divider ── */
.sdiv { display: flex; align-items: center; gap: 12px; margin: 6px 0 24px; }
.sdiv-line {
  flex: 1; height: 1px;
  background: linear-gradient(to right, rgba(168,32,32,.6), rgba(168,32,32,.05));
}
.sdiv-glyph { color: var(--gold-lo); font-size: .8rem; }

/* ── Content grid ── */
.content-grid { display: grid; grid-template-columns: 1fr 1.6fr; gap: 22px; }
.col { display: flex; flex-direction: column; gap: 22px; }

/* ── Card ── */
.card {
  background: rgba(26,18,12,.95);
  border: 1px solid rgba(168,32,32,.45);
  border-radius: 1px; padding: 26px 24px;
  position: relative; overflow: hidden;
  backdrop-filter: blur(10px);
  transition: border-color .4s, box-shadow .4s;
}
.card::before {
  content: '';
  position: absolute; inset: 0;
  background: linear-gradient(150deg, rgba(168,32,32,.05) 0%, transparent 50%);
  pointer-events: none;
}
.card:hover {
  border-color: rgba(168,32,32,.55);
  box-shadow: 0 0 40px rgba(168,32,32,.07), inset 0 0 40px rgba(168,32,32,.03);
}

/* Corner marks */
.cc { position: absolute; width: 10px; height: 10px; border-color: var(--gold-lo); border-style: solid; transition: border-color .4s; }
.card:hover .cc { border-color: var(--gold); }
.cc.tl { top: -1px;    left: -1px;  border-width: 1px 0 0 1px; }
.cc.tr { top: -1px;    right: -1px; border-width: 1px 1px 0 0; }
.cc.bl { bottom: -1px; left: -1px;  border-width: 0 0 1px 1px; }
.cc.br { bottom: -1px; right: -1px; border-width: 0 1px 1px 0; }

.card-title {
  font-family: 'Cinzel', serif;
  font-size: .58rem; font-weight: 600;
  letter-spacing: .26em; text-transform: uppercase;
  color: #d4aa50;
  display: flex; align-items: center; gap: 10px;
  margin-bottom: 4px;
}
.ct-num { font-size: .5rem; color: var(--blood); }

/* ── Skills ── */
.skills { display: flex; flex-wrap: wrap; gap: 9px; margin-top: 4px; }
.s-tag {
  display: flex; align-items: center; gap: 7px;
  background: rgba(168,32,32,.08);
  border: 1px solid rgba(168,32,32,.28);
  padding: 7px 14px; border-radius: 1px;
  font-family: 'Cinzel', serif; font-size: .55rem;
  letter-spacing: .14em; text-transform: uppercase;
  color: var(--bone); cursor: default;
  transition: background .3s, border-color .3s, color .3s, transform .2s;
  opacity: 0; animation: rise .5s ease forwards;
}
.s-tag:hover {
  background: rgba(168,32,32,.22);
  border-color: var(--blood); color: var(--white);
  transform: translateY(-2px);
}
.s-dot {
  width: 4px; height: 4px; border-radius: 50%;
  background: var(--blood); box-shadow: 0 0 6px rgba(168,32,32,.9); flex-shrink: 0;
}

/* ── Certs ── */
.cert {
  display: flex; gap: 14px; align-items: flex-start;
  padding: 14px 0; border-bottom: 1px solid rgba(168,32,32,.1);
}
.cert:first-of-type { padding-top: 6px; }
.cert:last-child { border-bottom: none; padding-bottom: 0; }
.cert-seal {
  width: 38px; height: 38px; flex-shrink: 0;
  border: 1px solid rgba(212,170,80,.3);
  background: rgba(168,32,32,.07);
  display: flex; align-items: center; justify-content: center;
  font-size: 1rem; color: var(--gold);
  text-shadow: 0 0 10px rgba(212,170,80,.5);
}
.cert-name { font-family: 'Cinzel', serif; font-size: .72rem; color: var(--white); margin-bottom: 3px; }
.cert-org  { font-size: .88rem; font-style: italic; color: #d45a5a; margin-bottom: 2px; }
.cert-date { font-size: .75rem; color: var(--smoke); }

/* ── Education ── */
.edu { display: flex; gap: 18px; position: relative; padding-bottom: 8px; }
.edu-spine { display: flex; flex-direction: column; align-items: center; }
.edu-rune {
  width: 16px; height: 16px; flex-shrink: 0;
  border: 1px solid var(--blood); background: var(--ink);
  display: flex; align-items: center; justify-content: center;
  font-size: .5rem; color: var(--blood);
  box-shadow: 0 0 10px rgba(168,32,32,.5);
  margin-top: 3px;
}
.edu-vline {
  flex: 1; width: 1px; margin-top: 5px; min-height: 36px;
  background: linear-gradient(to bottom, rgba(168,32,32,.5), transparent);
}
.edu-school { font-family: 'Cinzel', serif; font-size: .9rem; font-weight: 600; color: var(--white); margin-bottom: 5px; letter-spacing: .04em; }
.edu-deg   { font-size: .95rem; font-style: italic; color: var(--ghost); margin-bottom: 5px; }
.edu-dates { font-family: 'Cinzel', serif; font-size: .58rem; letter-spacing: .1em; color: #d45a5a; }

/* ── Projects ── */
.project {
  padding: 20px;
  border: 1px solid rgba(168,32,32,.18);
  background: rgba(168,32,32,.035);
  border-radius: 1px; margin-bottom: 14px;
  position: relative; overflow: hidden;
  transition: border-color .3s, background .3s;
}
.project:last-child { margin-bottom: 0; }
.project::before {
  content: '';
  position: absolute; top: 0; left: 0;
  width: 2px; height: 100%;
  background: linear-gradient(to bottom, var(--blood), transparent);
}
.project:hover { border-color: rgba(168,32,32,.45); background: rgba(168,32,32,.07); }

.proj-head { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 8px; gap: 10px; }
.proj-name  { font-family: 'Cinzel', serif; font-size: .9rem; font-weight: 600; color: var(--white); letter-spacing: .05em; }
.proj-dates { font-size: .78rem; color: var(--smoke); font-style: italic; white-space: nowrap; }
.proj-desc  { font-size: .96rem; line-height: 1.65; color: var(--ghost); font-style: italic; margin-bottom: 14px; }

.proj-status { display: flex; align-items: center; gap: 8px; }
.proj-status-label {
  font-family: 'Cinzel', serif; font-size: .48rem;
  letter-spacing: .2em; text-transform: uppercase; color: var(--gold);
}
.proj-status-label::before { content: '✝ '; color: var(--blood); }
.proj-bar { flex: 1; height: 1px; background: rgba(168,32,32,.15); overflow: hidden; }
.proj-bar-fill {
  height: 100%; width: 0;
  background: linear-gradient(90deg, var(--blood), rgba(168,32,32,.2));
  animation: fill 1.6s ease forwards 1s;
}
@keyframes fill { to { width: 70%; } }

/* ── Footer ── */
.footer {
  display: flex; flex-direction: column; align-items: center; gap: 10px;
  margin-top: 64px;
  opacity: 0; animation: rise .6s ease forwards 1.3s;
}
.footer-orn { display: flex; align-items: center; gap: 14px; width: 100%; }
.footer-line { flex: 1; height: 1px; background: linear-gradient(to right, transparent, rgba(168,32,32,.4), transparent); }
.footer-cross { font-size: 1.2rem; color: var(--blood); text-shadow: 0 0 12px rgba(168,32,32,.8); }
.footer-text { font-family: 'Cinzel', serif; font-size: .46rem; letter-spacing: .3em; color: var(--smoke); text-transform: uppercase; }

/* ── Responsive ── */
@media (max-width: 640px) {
  .hero { grid-template-columns: 1fr; gap: 28px; }
  .content-grid { grid-template-columns: 1fr; }
  .hero-name .ln { font-size: 2rem; }
}
</style>