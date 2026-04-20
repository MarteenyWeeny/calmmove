<template>
  <div class="personal-page-container">
    <header class="profile-header animate-in">
      <div class="avatar-container">
        <img :src="profileImage" alt="Profile Picture" class="profile-avatar" />
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
      <h2 class="section-title">Projects</h2>
      <div class="resume-item project-card" v-for="(project, index) in projects" :key="index">
        <h3 class="item-title">{{ project.name }} | <span class="item-dates-inline">{{ project.dates }}</span></h3>
        <p class="item-desc">{{ project.description }}</p>
      </div>
    </section>

    <section class="resume-section animate-in delay-4">
      <h2 class="section-title">Licenses and Certifications</h2>
      <div class="resume-item" v-for="(cert, index) in certifications" :key="index">
        <h3 class="item-title">{{ cert.name }}</h3>
        <p class="item-subtitle">{{ cert.issuer }}</p>
        <span class="item-dates">{{ cert.date }}</span>
      </div>
    </section>

    <section class="resume-section animate-in delay-5">
      <h2 class="section-title">Skills</h2>
      <ul class="skills-list">
        <li v-for="(skill, index) in skills" :key="index" class="skill-badge">{{ skill }}</li>
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
const profileImage = "/ppiangco.jpg" // Image must be inside public/ directory

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
/* Base Container Styles */
.personal-page-container {
  font-family: "Funnel Sans", Arial, Helvetica, sans-serif;
  color: #1e293b;
  max-width: 800px;
  margin: 0 auto;
  padding: 80px 20px; /* Top padding to clear fixed navbar */
  background-color: #f8fafc;
  overflow-x: hidden;
}

/* Animations Logic */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-in {
  opacity: 0;
  animation: fadeInUp 0.8s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.delay-1 { animation-delay: 0.1s; }
.delay-2 { animation-delay: 0.2s; }
.delay-3 { animation-delay: 0.3s; }
.delay-4 { animation-delay: 0.4s; }
.delay-5 { animation-delay: 0.5s; }

/* Profile Header with Hover Glow */
.profile-header {
  display: flex;
  align-items: center;
  gap: 25px;
  margin-bottom: 40px;
}

.avatar-container {
  width: 110px;
  height: 110px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid #0f766e; /* Using LetMCook Teal */
  transition: transform 0.4s ease, box-shadow 0.4s ease;
  box-shadow: 0 10px 25px -5px rgba(15, 118, 110, 0.2);
}

.avatar-container:hover {
  transform: scale(1.05) rotate(5deg);
  box-shadow: 0 15px 30px -5px rgba(15, 118, 110, 0.4);
}

.profile-name {
  font-size: 2.2em;
  font-weight: 800;
  background: linear-gradient(135deg, #0f766e, #84cc16); /* Teal to Lime gradient */
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* Interactive Section Cards */
.resume-section {
  margin-bottom: 30px;
  background-color: #ffffff;
  padding: 30px;
  border-radius: 16px;
  border: 1px solid #e2e8f0;
  transition: all 0.3s ease;
}

.resume-section:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
  border-color: #84cc16; /* Highlights with brand lime on hover */
}

.section-title {
  font-size: 1.1em;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 25px;
  color: #0f172a;
  border-left: 5px solid #0f766e;
  padding-left: 15px;
}

/* Project Cards */
.project-card {
  padding: 15px;
  border-radius: 8px;
  background: linear-gradient(to right, #ffffff, #f1f5f9);
  border-left: 2px solid transparent;
  transition: border-color 0.3s;
}

.project-card:hover {
  border-left-color: #0f766e;
}

/* Flashy Skills Badges */
.skills-list {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  padding: 0;
  list-style: none;
}

.skill-badge {
  background: #f1f5f9;
  color: #0f766e;
  padding: 8px 16px;
  border-radius: 99px;
  font-size: 0.9em;
  font-weight: 600;
  border: 1px solid #e2e8f0;
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.skill-badge:hover {
  background: #0f766e;
  color: #ffffff;
  transform: scale(1.1) translateY(-3px);
  box-shadow: 0 10px 15px -3px rgba(15, 118, 110, 0.3);
}

@media (max-width: 640px) {
  .profile-header {
    flex-direction: column;
    text-align: center;
  }
}
</style>