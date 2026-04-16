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

const fullName = "Geryme Vega"
const email = "24-1-01154@vsu.edu.ph"
const bio = "I enjoy watching movies and underrated animes in my spare time. I also play games!"
const profileImage = "/your-image-filename.png" // Image must be inside public/ directory

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
    degree: "Bachelor of Science in YYY",
    dates: "month year – month year"
  }
]

const projects = [
  {
    name: "Project Name",
    dates: "month year - month year",
    description: "Brief Description of the project."
  }
]

const certifications = [
  {
    name: "Certificate Name",
    issuer: "Certificate Issuer",
    date: "month year"
  }
]

const skills = [
  "Skill 1",
  "Skill 2",
  "Skill 3",
  "Skill 4"
]
</script>

<style scoped>
/* Step 8: Scoped CSS integrating your app's overarching theme */
.personal-page-container {
  font-family: "Funnel Sans", Arial, Helvetica, sans-serif;
  color: #111827;
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
  background-color: #f9fafb;
}

.profile-header {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 25px;
}

.avatar-container {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid #0f766e; /* Teal accent from navbar */
  background-color: #ffffff;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
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
  font-weight: bold;
  margin: 0 0 5px 0;
  color: #111827;
}

.profile-email {
  margin: 0;
  font-size: 1em;
  color: #6b7280; /* Footer gray */
}

.bio-section {
  margin-bottom: 40px;
  font-size: 1.05em;
  line-height: 1.6;
}

.resume-section {
  margin-bottom: 30px;
  background-color: #ffffff;
  padding: 25px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.05);
  border: 1px solid #e5e7eb;
}

.section-title {
  font-size: 1.3em;
  font-weight: bold;
  margin-top: 0;
  margin-bottom: 20px;
  color: #111827;
  border-left: 5px solid #84cc16; /* Lime green accent from nav-link hover */
  padding-left: 10px;
}

.resume-item {
  margin-bottom: 25px;
}

.resume-item:last-child {
  margin-bottom: 0;
}

.item-title {
  font-size: 1.1em;
  font-weight: bold;
  margin: 0 0 4px 0;
  color: #111827;
}

.item-subtitle {
  margin: 0 0 4px 0;
  font-size: 0.95em;
  color: #111827;
}

.item-dates {
  display: block;
  font-size: 0.85em;
  color: #6b7280;
  margin-bottom: 8px;
}

.item-dates-inline {
  font-size: 0.85em;
  font-weight: normal;
  color: #6b7280;
}

.item-desc {
  margin: 0;
  font-size: 0.95em;
  line-height: 1.5;
  color: #374151;
}

.skills-list {
  list-style-type: disc;
  padding-left: 20px;
  margin: 0;
  columns: 2; /* Automatically splits skills into two clean columns */
  column-gap: 40px;
}

.skills-list li {
  margin-bottom: 8px;
  font-size: 0.95em;
}
</style>