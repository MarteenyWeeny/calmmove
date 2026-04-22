<template>
  <div class="personal-page-container">
    <header class="profile-header">
      <div class="avatar-container">
        <img :src="profileImage" alt="Profile Picture" class="profile-avatar" />
      </div>
      
      <div class="profile-info">
        <h1 class="profile-name">{{ fullName }}</h1>
        <p class="profile-job">{{ jobDescription }}</p>
        <p class="profile-bio">{{ bio }}</p>
        <div class="profile-links">
          <a :href="portfolio" target="_blank" class="profile-link"> Sierra Bullones, Bohol</a>
          <a :href="linkedin" target="_blank" class="profile-link"> LinkedIn</a>
          <a :href="github" target="_blank" class="profile-link"> GitHub</a>
          <a :href="'mailto:' + email" class="profile-link"> e-mail</a>
        </div>
      </div>

      <section class="about-me-card">
        <h2 class="section-title">About Me</h2>
        <div v-for="(description, index) in AboutMe" :key="index">
          <p class="item-desc">{{ description.description }}</p>
        </div>
      </section>
    </header>

    <section class="resume-section">
      <h2 class="section-title">Educational Background</h2>
      <div class="education-grid">
        <div class="education-card" v-for="(edu, index) in education" :key="index">
          <h3 class="item-title">{{ edu.school }}</h3>
          <p class="item-subtitle">{{ edu.degree }}</p>
          <span class="item-dates">{{ edu.dates }}</span>
          <p class="item-relevance"><strong>Relevance:</strong> {{ edu.relevance }}</p>
        </div>
      </div>
    </section>

    <section class="resume-section">
      <h2 class="section-title">Projects</h2>
      <div class="projects-grid">
        <div class="project-card" v-for="(project, index) in projects" :key="index">
          <h3 class="item-title">{{ project.name }}</h3>
          <span class="item-dates">{{ project.dates }}</span>
          <p class="item-desc">{{ project.description }}</p>
        </div>
      </div>
    </section>

    <section class="resume-section">
      <h2 class="section-title">Skills</h2>
      <div class="skills-grid">
        <div class="skill-category-card" v-for="(items, category) in skills" :key="category">
          <h3 class="item-title category-name">{{ category }}</h3>
          <ul class="skills-list">
            <li v-for="skill in items" :key="skill">{{ skill }}</li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { useHead } from '#imports'

const fullName = "Liza Mae G. Caduyac"
const jobDescription = "Full Stack Web Developer | Computer Science Student"
const bio = "Building Seamless Digital Experiences from Pixel to Production."
const email = "23-1-02225@vsu.edu.ph"
const linkedin = "https://www.linkedin.com/in/liza-mae-caduyac-55377b3a9/" 
const github = "https://github.com/Zaming" 
const portfolio = "https://www.google.com/maps/place/Sierra+Bullones,+Bohol/@9.7923049,124.2496849,13z/data=!3m1!4b1!4m6!3m5!1s0x33aa118cb8b36331:0xe8ae11b37e301512!8m2!3d9.7807194!4d124.297718!16zL20vMDZsZ19t?entry=ttu&g_ep=EgoyMDI2MDQxOS4wIKXMDSoASAFQAw%3D%3D"
const profileImage = "/lmcaduyac.png" 

useHead({
  title: fullName,
  meta: [ { name: 'description', content: `The personal page of ${fullName}.` } ]
})

const AboutMe = [
  { description: "Passionate about crafting seamless user experiences and efficient backend solutions. Skilled in JavaScript, Python, and modern web frameworks. Dedicated to continuous learning and delivering high-quality code." }
]

const education = [
  { school: "Visayas State University", degree: "Bachelor of Science in Computer Science", dates: "August 2023 – Present", relevance: "Focusing on Software Engineering, Data Structures, and Web Development." },
  { school: "Sierra Bullones Technical Vocational High School", degree: "Senior High School - STEM Strand", dates: "2021 – 2023", relevance: "Foundation in Advanced Mathematics (Pre-Calculus and basic Calculus) and Physics." }
]

const projects = [
  { name: "LetMCook", dates: "March 2026 - Present", description: "Smart meal planner using your ingredients to meet nutrient goals." },
  { name: "Winion", dates: "February 2026 - Present", description: "A platform that helps elder to navigate daily routines and lifetime commitment." }
]

// UPDATED SKILLS DATA STRUCTURE
const skills = {
  Languages: ["C/C++", "TypeScript", "Java", "Python", "JavaScript"],
  Tools: ["Git", "GitHub", "VS Code", "Node.js", "Vue.js", "Nuxt.js"],
  Knowledge: ["Web Development", "Data Structures", "UI/UX Design", "Database Management"]
}
</script>

<style scoped>
/* ... Keep your existing styles ... */

.personal-page-container {
  width: 100%;
  max-width: 100%;
  margin: 0;
  padding: 40px;
  display: flex;
  flex-direction: column;
  gap: 30px;
  background-color: #000000;
  box-sizing: border-box;
}

.profile-header {
  display: flex;
  gap: 30px;
  align-items: stretch;
  margin-bottom: 40px;
  width: 100%;
}

.avatar-container {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid #25F4EE;
  background-color: #FE2C55;
  box-shadow: 0 4px 15px rgba(37, 244, 238, 0.3);
  flex-shrink: 0;
}

.profile-avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  flex: 0 1 auto;
}

.profile-name {
  font-size: 3em;
  font-weight: bold;
  margin: 0 0 5px 0;
  color: #ffffff;
  font-family: 'Times New Roman', serif;
}

.profile-job {
  margin: 0 0 5px 0;
  font-size: 1.5em;
  color: #ffffff;
}

.profile-bio {
  margin: 0 0 10px 0;
  font-size: 1em;
  color: #ffffff;
  font-style: italic;
}

.profile-link {
  display: inline-block;
  margin-right: 15px;
  color: #000000;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9em;
  background-color: #ffffff;
  padding: 8px 16px;
  border-radius: 20px;
  border: 2px solid #25F4EE;
  transition: all 0.3s ease;
}

.profile-link:hover {
  background-color: #FE2C55;
  color: #ffffff;
  border-color: #ffffff;
}

.resume-section {
  margin-bottom: 30px;
  background-color: #1a1a1a;
  padding: 30px;
  border-radius: 15px;
  border: 1px solid #333333;
}

.section-title {
  font-size: 1.4em;
  font-weight: bold;
  margin-bottom: 25px;
  color: #ffffff;
  font-family: 'Times New Roman', serif;
  display: flex;
  align-items: center;
  gap: 15px;
}

.section-title::before {
  content: "";
  width: 40px;
  height: 10px;
  background: radial-gradient(circle, #FE2C55 4px, transparent 5px) 0% 50%,
              radial-gradient(circle, #FFFFFF 4px, transparent 5px) 50% 50%,
              radial-gradient(circle, #25F4EE 4px, transparent 5px) 100% 50%;
  background-size: 14px 10px;
  background-repeat: no-repeat;
  display: inline-block;
  flex-shrink: 0;
}

/* NEW SKILLS GRID STYLING */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Three columns for 3 boxes */
  gap: 20px;
}

.skill-category-card {
  background-color: #2d2d2d; /* Match the other cards */
  border: 2px solid #25F4EE;
  border-radius: 12px;
  padding: 20px;
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.skill-category-card:hover {
  transform: translateY(-5px);
  border-color: #FE2C55;
  box-shadow: 0 10px 20px rgba(37, 244, 238, 0.1);
}

.category-name {
  text-transform: capitalize;
  border-bottom: 1px solid #444;
  padding-bottom: 10px;
  margin-bottom: 15px;
}

.skills-list {
  list-style: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.skills-list li {
  color: #ffffff;
  background-color: #0f766e;
  border: 2px solid #25F4EE;
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.85em;
  font-weight: 500;
  transition: all 0.3s ease;
}

.skills-list li:hover {
  background-color: #FE2C55;
  transform: scale(1.05);
}

/* Reusing your existing grid/card styles */
.education-grid, .projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.education-card, .project-card, .about-me-card {
  background-color: #2d2d2d;
  border: 2px solid #25F4EE;
  border-radius: 12px;
  padding: 25px;
  color: #ffffff;
  transition: transform 0.2s ease, border-color 0.2s ease;
  flex: 1;
}

.education-card:hover, .project-card:hover {
  transform: translateY(-5px);
  border-color: #FE2C55;
}

.item-title { color: #ffffff; font-size: 1.2em; margin-bottom: 5px; }
.item-subtitle { color: #25F4EE; font-weight: 500; margin-bottom: 5px; }
.item-dates { color: #b3b3b3; font-size: 0.85em; display: block; margin-bottom: 10px; }
.item-desc, .item-relevance { color: #ffffff; line-height: 1.6; font-size: 0.95em; }

@media (max-width: 1024px) {
  .profile-header { flex-direction: column; }
  .education-grid, .projects-grid, .skills-grid { grid-template-columns: 1fr; }
}
</style>