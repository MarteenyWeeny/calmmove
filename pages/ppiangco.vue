<template>
  <div class="personal-page-container">
    <header class="profile-header">
      <div class="avatar-container">
        <img :src="profileImage" alt="Profile Picture" class="profile-avatar" />
      </div>
      <div class="profile-info">
        <h1 class="profile-name">{{ fullName }}</h1>
        <p class="profile-email">{{ email }}</p>
      </div>
    </header>

    <section class="bio-section">
      <p>{{ bio }}</p>
    </section>

    <section class="resume-section">
      <h2 class="section-title">Educational Background</h2>
      <div class="resume-item" v-for="(edu, index) in education" :key="index">
        <h3 class="item-title">{{ edu.school }}</h3>
        <p class="item-subtitle">{{ edu.degree }}</p>
        <span class="item-dates">{{ edu.dates }}</span>
      </div>
    </section>

    <section class="resume-section">
      <h2 class="section-title">Projects</h2>
      <div class="resume-item" v-for="(project, index) in projects" :key="index">
        <h3 class="item-title">{{ project.name }} | <span class="item-dates-inline">{{ project.dates }}</span></h3>
        <p class="item-desc">{{ project.description }}</p>
      </div>
    </section>

    <section class="resume-section">
      <h2 class="section-title">Licenses and Certifications</h2>
      <div class="resume-item" v-for="(cert, index) in certifications" :key="index">
        <h3 class="item-title">{{ cert.name }}</h3>
        <p class="item-subtitle">{{ cert.issuer }}</p>
        <span class="item-dates">{{ cert.date }}</span>
      </div>
    </section>

    <section class="resume-section">
      <h2 class="section-title">Skills</h2>
      <ul class="skills-list">
        <li v-for="(skill, index) in skills" :key="index">{{ skill }}</li>
      </ul>
    </section>
  </div>
</template>

<script setup>
import { useHead } from '#imports' // Adjust if not using Nuxt auto-imports

// ==========================================
// MEMBER CONFIGURATION: Edit details below
// ==========================================

const fullName = "Pete Alexander Piangco"
const email = "24-1-01218@vsu.edu.ph"
const bio = "I turn complex ideas into high-impact software, leveraging a foundation in system design and algorithms to ship fast, reliable, and meticulously crafted digital experiences. I also like cats"
const profileImage = "/ppiangco.png" // Image must be inside public/ directory

// Steps 4 & 5: Set Page Title and Description automatically
useHead({
  title: fullName,
  meta: [
    { name: 'description', content: `The personal page of ${fullName}.` }
  ]
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

const certifications = [
  {
    name: "CS Week 2nd Runner Up",
    issuer: "Computer Science Students Society",
    date: "February 2026"
  }
]

const skills = [
  "React",
  "Java",
  "Python",
  "C/C++"
]
</script>

<style scoped>
/* Step 8: Scoped CSS integrating your app's overarching theme */
.personal-page-container {
  font-family: "Funnel Sans", Arial, Helvetica, sans-serif;
  color: #1e293b; /* Slate 800 for better readability */
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
  background-color: #f8fafc; /* Very light slate blue-gray background */
}

.profile-header {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
}

.avatar-container {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  overflow: hidden;
  border: 2px solid #0f172a; /* Deep Navy border */
  background-color: #ffffff;
  box-shadow: 0 10px 15px -3px rgba(15, 23, 42, 0.1);
}

.profile-avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-info {
  display: flex;
  flex-direction: column;
}

.profile-name {
  font-size: 1.8em;
  font-weight: 800;
  margin: 0 0 5px 0;
  color: #0f172a; /* Deep Navy */
}

.profile-email {
  margin: 0;
  font-size: 0.95em;
  color: #64748b; /* Muted Slate */
  letter-spacing: 0.02em;
}

.bio-section {
  margin-bottom: 40px;
  font-size: 1.05em;
  line-height: 1.7;
  color: #334155;
}

.resume-section {
  margin-bottom: 30px;
  background-color: #ffffff;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
  border: 1px solid #e2e8f0;
}

.section-title {
  font-size: 1.1em;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-top: 0;
  margin-bottom: 25px;
  color: #1e293b;
  border-left: 4px solid #0f172a; /* Deep Navy accent */
  padding-left: 15px;
}

.resume-item {
  margin-bottom: 25px;
}

.resume-item:last-child {
  margin-bottom: 0;
}

.item-title {
  font-size: 1.1em;
  font-weight: 700;
  margin: 0 0 4px 0;
  color: #0f172a;
}

.item-subtitle {
  margin: 0 0 4px 0;
  font-size: 0.95em;
  font-weight: 500;
  color: #475569;
}

.item-dates {
  display: block;
  font-size: 0.85em;
  color: #94a3b8;
  margin-bottom: 10px;
  font-weight: 500;
}

.item-desc {
  margin: 0;
  font-size: 0.95em;
  line-height: 1.6;
  color: #334155;
}

.skills-list {
  list-style-type: none; /* Removed discs for a cleaner look */
  padding-left: 0;
  margin: 0;
  columns: 2;
  column-gap: 40px;
}

.skills-list li {
  margin-bottom: 10px;
  font-size: 0.9em;
  color: #334155;
  padding-left: 15px;
  position: relative;
}

/* Custom minimal bullet for skills */
.skills-list li::before {
  content: "";
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 4px;
  height: 4px;
  background-color: #cbd5e1;
  border-radius: 50%;
}
</style>