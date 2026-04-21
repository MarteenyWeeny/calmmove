<template>
  <div class="personal-page-wrapper">
    <div class="personal-page-container">
      <header class="profile-header animate-in">
        <div class="avatar-container">
          <img :src="profileImage" alt="Pete Alexander Piangco" class="profile-avatar" />
        </div>
        <div class="profile-info">
          <h1 class="profile-name">{{ fullName }}</h1>
          <p class="profile-email">{{ email }}</p>
        </div>
      </header>

      <section class="bio-section animate-in delay-1">
        <p>{{ bio }}</p>
      </section>

      <section class="resume-section animate-in delay-2">
        <h2 class="section-title">Educational Background</h2>
        <div class="resume-item" v-for="(edu, index) in education" :key="index">
          <h3 class="item-title">{{ edu.school }}</h3>
          <p class="item-subtitle">{{ edu.degree }}</p>
          <span class="item-dates">{{ edu.dates }}</span>
        </div>
      </section>

      <section class="resume-section animate-in delay-3">
        <h2 class="section-title">Experience & Projects</h2>
        <div class="resume-item project-card" v-for="(project, index) in projects" :key="index">
          <h3 class="item-title">{{ project.name }} | <span class="item-dates-inline">{{ project.dates }}</span></h3>
          <p class="item-desc">{{ project.description }}</p>
        </div>
      </section>

      <section class="resume-section animate-in delay-4">
        <h2 class="section-title">Technical Expertise</h2>
        <div class="skills-matrix">
          <div class="skill-category" v-for="(cat, cIndex) in categorizedSkills" :key="cIndex">
            <h3 class="category-label">{{ cat.label }}</h3>
            <div class="skills-grid">
              <span v-for="(skill, sIndex) in cat.items" :key="sIndex" :class="['skill-pill-dynamic', cat.tagClass]">
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
import { useHead } from '#imports'

const fullName = "Pete Alexander Piangco"
const email = "24-1-01218@vsu.edu.ph"
const bio = "I turn complex ideas into high-impact software, leveraging a foundation in system design and algorithms to ship fast, reliable, and meticulously crafted digital experiences. I also like cats"
const profileImage = "/ppiangco.jpg"

useHead({
  title: fullName,
  meta: [{ name: 'description', content: `Personal portfolio of ${fullName}.` }]
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
    dates: "March 2026 - Present",
    description: "Smart meal planner using your ingredients to meet nutrient goals."
  }
]

const categorizedSkills = [
  { label: "Languages", tagClass: "language-tag", items: ["C/C++", "Java", "SQL", "JavaScript", "HTML/CSS"] },
  { label: "Technologies & Tools", tagClass: "tech-tag", items: ["Git", "VS Code", "MySQL", "React", "Vue.js / Nuxt"] },
  { label: "Core Competencies", tagClass: "soft-tag", items: ["Problem-Solving", "Critical Thinking", "Leadership", "Collaboration"] }
]
</script>

<style scoped>
/* Base Styles */
.personal-page-wrapper {
  background: #f8fafc;
  min-height: 100vh;
}

.personal-page-container {
  font-family: "Funnel Sans", sans-serif;
  /* */
  max-width: 800px;
  margin: 0 auto;
  padding: 80px 20px;
}

/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-in {
  opacity: 0;
  animation: fadeInUp 0.6s ease-out forwards;
}

.delay-1 {
  animation-delay: 0.1s;
}

.delay-2 {
  animation-delay: 0.2s;
}

.delay-3 {
  animation-delay: 0.3s;
}

.delay-4 {
  animation-delay: 0.4s;
}

/* Header and Matrix */
.profile-header {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
}

.avatar-container {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid #0f766e;
}

.profile-name {
  color: #0f766e;
  font-size: 2rem;
  margin: 0;
}

.resume-section {
  background: white;
  padding: 30px;
  border-radius: 12px;
  margin-bottom: 25px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.section-title {
  color: #0f766e;
  border-left: 4px solid #84cc16;
  padding-left: 15px;
  text-transform: uppercase;
  font-size: 1rem;
}

/* Skills Matrix */
.skills-matrix {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.skill-pill-dynamic {
  display: inline-block;
  padding: 6px 12px;
  margin: 4px;
  border-radius: 6px;
  font-weight: 600;
  transition: all 0.3s;
}

.language-tag {
  background: #f0fdfa;
  color: #0f766e;
}

.tech-tag {
  background: #f7fee7;
  color: #84cc16;
}

.soft-tag {
  background: #f8fafc;
  color: #64748b;
}

.skill-pill-dynamic:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
</style>