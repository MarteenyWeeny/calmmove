<template>
  <div class="gvega-modern-container" :class="{ 'dark-mode-active': isDark }">
    <div class="resume-wrapper">
      
      <aside class="profile-sidebar">
        <div class="profile-card-inner">
          <div class="avatar-wrapper">
            <img :src="profileImage" alt="Geryme Vega Profile" class="profile-avatar" />
          </div>
          
          <div class="profile-intro">
            <h1 class="profile-name">{{ fullName }}</h1>
            <h2 class="profile-title">Student at VSU-Main</h2>
            
            <button class="email-chip" @click="copyEmail">
              <span class="email-text">{{ email }}</span>
              <transition name="fade" mode="out-in">
                <span v-if="emailCopied" key="success" class="copy-success">Copied! ✓</span>
                <span v-else key="hint" class="copy-hint">Click to copy</span>
              </transition>
            </button>
          </div>

          <div class="profile-bio">
            <p>{{ bio }}</p>
          </div>

          <div class="sidebar-footer">
            <button class="theme-toggle" @click="toggleTheme">
              <span v-if="!isDark">☀️ Light Mode</span>
              <span v-else>🌙 Dark Mode</span>
            </button>
          </div>
        </div>
      </aside>

      <main class="resume-main">
        
        <section class="content-group">
          <h2 class="group-label">Work & Technical Experience</h2>
          <div class="item-stack">
            <div class="modern-card" v-for="(exp, index) in experience" :key="index">
              <div class="card-accent"></div>
              <div class="card-body">
                <div class="card-header">
                  <h3 class="card-title">{{ exp.role }}</h3>
                  <span class="card-tag">{{ exp.dates }}</span>
                </div>
                <p class="card-subtitle">{{ exp.company }}</p>
                <p class="card-text">{{ exp.desc }}</p>
              </div>
            </div>
          </div>
        </section>

        <section class="content-group">
          <h2 class="group-label">Educational Background</h2>
          <div class="item-stack">
            <div class="modern-card" v-for="(edu, index) in education" :key="index">
              <div class="card-accent"></div>
              <div class="card-body">
                <div class="card-header">
                  <h3 class="card-title">{{ edu.school }}</h3>
                  <span class="card-tag">{{ edu.dates }}</span>
                </div>
                <p class="card-subtitle">{{ edu.degree }}</p>
                <p class="card-text italic">{{ edu.desc }}</p>
              </div>
            </div>
          </div>
        </section>

        <section class="content-group">
          <h2 class="group-label">Projects</h2>
          <div class="item-stack">
            <div class="modern-card project-interaction" v-for="(project, index) in projects" :key="index">
              <div class="card-body">
                <div class="card-header">
                  <h3 class="card-title">{{ project.name }}</h3>
                  <span class="card-tag">{{ project.dates }}</span>
                </div>
                <p class="card-text">{{ project.description }}</p>
              </div>
            </div>
          </div>
        </section>

        <div class="split-row">
          <section class="content-group">
            <h2 class="group-label">Certifications</h2>
            <div class="item-stack">
              <div class="mini-card" v-for="(cert, index) in certifications" :key="index">
                <h3 class="card-title small">{{ cert.name }}</h3>
                <p class="card-subtitle small">{{ cert.issuer }}</p>
                <p class="credential-id">ID: {{ cert.id }}</p>
              </div>
            </div>
          </section>

          <section class="content-group">
            <h2 class="group-label">Skills</h2>
            <div class="skills-grid">
              <button 
                class="interactive-tag" 
                v-for="(skill, index) in skills" 
                :key="index"
                :class="{ 'tag-active': activeSkills.includes(skill) }"
                @click="toggleSkill(skill)"
              >
                {{ skill }}
              </button>
            </div>
          </section>
        </div>

      </main>
    </div>
  </div>
</template>

<script setup>
import { useHead } from '#imports'
import { ref } from 'vue'

const fullName = "Geryme M. Vega"
const email = "24-1-01154@vsu.edu.ph"
const bio = "DOST-SEI Scholar and competitive programmer with training in Algorithms and Data Structures. I engineer low-level C++ solutions to optimize memory and runtime efficiency."
const profileImage = "/gvega.png"

useHead({
  title: fullName,
  meta: [{ name: 'description', content: `The personal page of ${fullName}.` }]
})

const isDark = ref(false)
const toggleTheme = () => { isDark.value = !isDark.value }

const emailCopied = ref(false)
const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText(email)
    emailCopied.value = true
    setTimeout(() => { emailCopied.value = false }, 2000)
  } catch (err) { console.error(err) }
}

const activeSkills = ref([])
const toggleSkill = (skill) => {
  activeSkills.value.includes(skill) 
    ? activeSkills.value = activeSkills.value.filter(s => s !== skill)
    : activeSkills.value.push(skill)
}

const experience = [
  { role: "Competitive Programmer", company: "HackerRank & LeetCode", dates: "Nov 2025", desc: "Solved 100+ challenges focusing on low-level optimization." },
  { role: "Bronze Medalist (Heat Round)", company: "PIMO", dates: "Apr 2023", desc: "Applied mathematical knowledge to combinatorial problems." }
]

const education = [
  { school: "Visayas State University", degree: "Bachelor of Science in Computer Science", dates: "2024 – 2028", desc: "DOST-SEI Scholar (RA 7687): Scored in the top 11% nationwide." }
]

const projects = [
  { name: "EcoBayan (1st Place, RSCENE 2025)", dates: "June 2025", description: "Spearheaded R&D of a waste management app projected to increase efficiency by 50%." },
  { name: "Custom Data Structures Library", dates: "Nov 2025", description: "Engineered a low-level C++ library, achieving a 90% improvement in retrieval speeds." }
]

const certifications = [
  { name: "Algorithms & Data Structures", issuer: "HackerRank", date: "2025", id: "EA9990A7F219" },
  { name: "AWS Machine Learning", issuer: "Skillsoft", date: "2025", id: "147061247" }
]

const skills = ["C/C++", "Python", "Java", "DSA", "Memory Mgmt", "Linux", "Git", "DaVinci Resolve"]
</script>

<style scoped>
.gvega-modern-container {
  --primary: #0f766e;
  --accent: #84cc16;
  --bg: #f8fafc;
  --card-bg: #ffffff;
  --text-main: #1e293b;
  --text-muted: #64748b;
  --border: rgba(15, 118, 110, 0.1);
  --shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05);
  
  font-family: "Funnel Sans", sans-serif;
  background-color: var(--bg);
  min-height: 100vh;
  padding: 40px 20px;
  display: flex;
  justify-content: center;
  transition: all 0.3s ease;
}

.dark-mode-active {
  --bg: #0f172a;
  --card-bg: #1e293b;
  --text-main: #f1f5f9;
  --text-muted: #94a3b8;
  --border: rgba(255, 255, 255, 0.05);
  --shadow: 0 10px 15px -3px rgb(0 0 0 / 0.3);
}

.resume-wrapper {
  display: grid;
  grid-template-columns: 350px 1fr;
  gap: 30px;
  max-width: 1200px;
  width: 100%;
}

.profile-sidebar {
  position: sticky;
  top: 40px;
  height: fit-content;
}

.profile-card-inner {
  background: var(--card-bg);
  border-radius: 30px;
  padding: 40px;
  box-shadow: var(--shadow);
  border: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.avatar-wrapper {
  width: 150px;
  height: 150px;
  border-radius: 40px;
  padding: 5px;
  background: linear-gradient(135deg, var(--primary), var(--accent));
  margin-bottom: 24px;
  transform: rotate(-3deg);
}

.profile-avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 35px;
  background: white;
  transform: rotate(3deg);
}

.profile-name { font-size: 1.8em; font-weight: 800; color: var(--text-main); margin: 0; }
.profile-title { 
  font-size: 1em; color: var(--primary); font-weight: 700; 
  margin: 10px 0 20px; padding: 5px 15px; background: rgba(15, 118, 110, 0.05);
  border-radius: 10px;
}

/* REFINED EMAIL CHIP STYLING */
.email-chip {
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 12px 20px;
  border-radius: 15px;
  cursor: pointer;
  width: 100%;
  position: relative;
  transition: all 0.2s ease;
}

.email-chip:hover {
  border-color: var(--primary);
  background: var(--card-bg);
}

.email-text { font-size: 0.9em; font-weight: 700; color: var(--primary); }

.copy-hint { 
  font-size: 0.7em; 
  display: block; 
  margin-top: 4px; 
  color: var(--text-muted);
  opacity: 0; /* Hidden by default */
  transform: translateY(-5px);
  transition: all 0.2s ease;
}

.email-chip:hover .copy-hint { 
  opacity: 1; 
  transform: translateY(0); 
}

.copy-success { 
  font-size: 0.7em; 
  display: block; 
  margin-top: 4px; 
  color: var(--accent); 
  font-weight: 800; 
}

/* FADE TRANSITION DEFINITION */
.fade-enter-active, .fade-leave-active { transition: opacity 0.3s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

.profile-bio { margin-top: 30px; font-size: 0.95em; line-height: 1.6; color: var(--text-muted); }

.sidebar-footer { margin-top: 40px; width: 100%; }
.theme-toggle {
  width: 100%; padding: 12px; border-radius: 15px; border: 2px solid var(--primary);
  background: transparent; color: var(--primary); font-weight: 700; cursor: pointer;
}

.resume-main { display: flex; flex-direction: column; gap: 40px; }

.group-label {
  font-size: 1.2em; font-weight: 800; color: var(--text-main);
  margin-bottom: 20px; display: flex; align-items: center; gap: 10px;
}
.group-label::after { content: ""; flex: 1; height: 2px; background: var(--border); }

.item-stack { display: flex; flex-direction: column; gap: 15px; }

.modern-card {
  background: var(--card-bg);
  border-radius: 20px;
  padding: 25px;
  box-shadow: var(--shadow);
  border: 1px solid var(--border);
  position: relative;
  overflow: hidden;
  transition: transform 0.2s ease;
}
.modern-card:hover { transform: translateY(-3px); }

.card-accent { 
  position: absolute; left: 0; top: 0; bottom: 0; width: 5px; background: var(--accent); 
}

.card-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
.card-title { font-size: 1.1em; font-weight: 700; color: var(--text-main); margin: 0; }
.card-title.small { font-size: 0.95em; }
.card-tag { font-size: 0.8em; font-weight: 700; color: var(--primary); background: rgba(15, 118, 110, 0.05); padding: 4px 12px; border-radius: 8px; }

.card-subtitle { font-size: 0.95em; font-weight: 600; color: var(--primary); margin: 0 0 10px; }
.card-text { font-size: 0.9em; line-height: 1.6; color: var(--text-muted); margin: 0; }
.italic { font-style: italic; }

.split-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }

.mini-card { 
  background: var(--card-bg); border-radius: 15px; padding: 15px; 
  box-shadow: var(--shadow); border: 1px solid var(--border); 
  margin-bottom: 10px; transition: all 0.3s ease;
}

.mini-card:hover { transform: translateY(-5px); border-color: var(--accent); }

.credential-id {
  font-size: 0.75em; font-family: monospace; color: var(--primary);
  margin-top: 8px; background: rgba(15, 118, 110, 0.05); padding: 4px 8px; border-radius: 5px; display: inline-block;
}

.skills-grid { display: flex; flex-wrap: wrap; gap: 10px; }
.interactive-tag {
  background: var(--card-bg); border: 1px solid var(--border); padding: 8px 16px;
  border-radius: 12px; font-size: 0.85em; font-weight: 600; color: var(--text-muted);
  cursor: pointer; transition: all 0.2s ease;
}
.interactive-tag:hover { border-color: var(--accent); color: var(--accent); }
.tag-active { background: var(--accent) !important; color: white !important; border-color: var(--accent) !important; }

@media (max-width: 1000px) {
  .resume-wrapper { grid-template-columns: 1fr; }
  .profile-sidebar { position: static; }
  .split-row { grid-template-columns: 1fr; }
}
</style>