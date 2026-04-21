<script lang="ts"></script>

<template>
  <client-only>
    <NavBar />
    <div id="CMMain" class="CM-main">
      <div class="tos-container">
        <div class="tos-content">
          <h1>Terms of Service (ToS)</h1>
          <p class="effective-date"><strong>Effective Date:</strong> March 11, 2026</p>
          
          <p>By accessing or using the LetMCook App, you agree to these Terms of Service ("ToS") and our Privacy Policy. If you do not agree, do not use the App.</p>

          <hr />

          <h2>1. Purpose of the App</h2>
          <p>The App provides personalized recipe suggestions and nutrient tracking based on the ingredients in your pantry and your dietary goals.</p>

          <h2>2. Eligibility</h2>
          <p>You must be at least 18 years old or the age of majority in your jurisdiction to use the App.</p>

          <h2>3. User Account</h2>
          <ul>
            <li>You are responsible for providing accurate information about yourself, including dietary preferences, height, weight, and daily nutrition goals.</li>
            <li>You are responsible for maintaining the confidentiality of your account credentials.</li>
          </ul>

          <h2>4. User Data and Privacy</h2>
          <p>The App collects personal and sensitive information including:</p>
          <ul>
            <li>Personal details (age, weight, height)</li>
            <li>Pantry inventory and meal history</li>
            <li>Dietary preferences and nutrient intake</li>
          </ul>

          <p><strong>Use of Data:</strong></p>
          <ul>
            <li>To generate personalized recipe suggestions and nutrient tracking.</li>
            <li>To improve the App's functionality and analytics.</li>
            <li>To communicate with you regarding App updates or features.</li>
          </ul>

          <p><strong>Legal Compliance:</strong></p>
          <ul>
            <li><strong>GDPR:</strong> Users in the EU have rights to access, correct, delete, or restrict processing of their personal data. You may request your data or withdraw consent at any time.</li>
            <li><strong>Philippine DPA:</strong> Personal data is processed lawfully, fairly, and securely. Users have the right to access, correct, and request deletion of their personal data.</li>
          </ul>

          <p><strong>Data Sharing:</strong></p>
          <ul>
            <li>We do <strong>not sell</strong> your personal data.</li>
            <li>Data may be shared with third-party service providers only to the extent necessary to operate the App (e.g., cloud hosting).</li>
          </ul>

          <h2>5. User Responsibilities</h2>
          <ul>
            <li>You must not provide false, inaccurate, or misleading information.</li>
            <li>You agree not to use the App to engage in unlawful activities or violate the rights of others.</li>
          </ul>

          <h2>6. Intellectual Property</h2>
          <ul>
            <li>All App content, recipes, logos, and designs are the property of LetMCook.</li>
            <li>You may not reproduce, distribute, or create derivative works without permission.</li>
          </ul>

          <h2>7. Limitation of Liability</h2>
          <ul>
            <li>The App provides nutritional information for general guidance only. It <strong>does not replace professional medical or dietary advice</strong>.</li>
            <li>LetMCook is not liable for any health issues, losses, or damages arising from the use of the App.</li>
          </ul>

          <h2>8. Termination</h2>
          <p>We may suspend or terminate your account for violations of these ToS.</p>
          <p>You may delete your account at any time, which will remove your personal data from the App in compliance with GDPR and DPA regulations.</p>

          <h2>9. Modifications</h2>
          <p>We may update these ToS at any time. Users will be notified of significant changes via email or in-app notifications. Continued use of the App constitutes acceptance of the revised ToS.</p>

          <h2>10. Governing Law</h2>
          <ul>
            <li><strong>EU Users:</strong> GDPR applies; local EU law also governs.</li>
            <li><strong>Philippine Users:</strong> Data Privacy Act of 2012 applies; Philippine law governs disputes.</li>
            <li><strong>Other jurisdictions:</strong> Governed by applicable local laws.</li>
          </ul>

          <h2>11. Contact</h2>
          <p>For questions or to exercise your data rights:</p>
          <p><strong>Email:</strong> <a href="mailto:martin9876543219@gmail.com">martin9876543219@gmail.com</a></p>
          <p><strong>Address:</strong> Baybay City, Leyte</p>

          <hr />

          <p class="last-updated"><em>Last updated: March 11, 2026</em></p>
        </div>
      </div>
    </div>
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
const title = "LetMCook | Terms of Service";
const description =
  "Terms and conditions for using LetMCook - Smart meal planner using your ingredients to meet nutrient goals.";

useSeoMeta({
  title: () => title,
  description: () => description,
  charset: "utf-8",
  viewport: "width=device-width, initial-scale=1.0",
});

useHead({
  link: [
    { rel: "icon", type: "image/png", href: "/logo.png" },
    { rel: "stylesheet", href: "/reset.css" },
    { rel: "stylesheet", href: "/custom.css" },
    { rel: "preconnect", href: "https://fonts.googleapis.com" },
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Funnel+Sans:ital,wght@0,300..800;1,300..800&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap",
    },
  ],
});
</script>

<style scoped>
.tos-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem 1.5rem;
}

.tos-content {
  background: white;
  border-radius: 12px;
  padding: 2rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  font-family: 'Roboto', sans-serif;
}

.tos-content h1 {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #1a1a1a;
}

.tos-content .effective-date {
  color: #666;
  margin-bottom: 1.5rem;
}

.tos-content h2 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-top: 2rem;
  margin-bottom: 1rem;
  color: #2a2a2a;
  border-bottom: 1px solid #e5e5e5;
  padding-bottom: 0.5rem;
}

.tos-content p {
  line-height: 1.6;
  margin-bottom: 1rem;
  color: #4a4a4a;
}

.tos-content ul {
  margin-bottom: 1rem;
  padding-left: 1.5rem;
}

.tos-content li {
  line-height: 1.6;
  margin-bottom: 0.5rem;
  color: #4a4a4a;
}

.tos-content strong {
  font-weight: 600;
  color: #1a1a1a;
}

.tos-content a {
  color: #4CAF50;
  text-decoration: none;
}

.tos-content a:hover {
  text-decoration: underline;
}

.tos-content hr {
  margin: 2rem 0;
  border: none;
  border-top: 1px solid #e5e5e5;
}

.tos-content .last-updated {
  text-align: right;
  color: #888;
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .tos-container {
    padding: 1rem;
  }
  
  .tos-content {
    padding: 1.5rem;
  }
  
  .tos-content h1 {
    font-size: 1.75rem;
  }
  
  .tos-content h2 {
    font-size: 1.25rem;
  }
}
</style>