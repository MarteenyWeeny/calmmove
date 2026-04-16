<script lang="ts"></script>

<template>
  <client-only>
    <NavBar />
    <main id="CMMain" class="CM-main">
      <article>
        <header>
          <h1>Privacy Policy – LetMCook</h1>
          <p><strong>Effective Date:</strong> March 11, 2026</p>
        </header>

        <section>
          <p>At LetMCook App, your privacy is important.</p>
          <p>This Privacy Policy explains how we collect, use, store, and protect your personal data in accordance with the <strong>EU General Data Protection Regulation (GDPR)</strong> and the <strong>Philippine Data Privacy Act of 2012 (DPA)</strong>.</p>
          <p>By using the App, you consent to the practices described here.</p>
        </section>

        <section>
          <h2>1. Information We Collect</h2>
          <p>We collect information you provide and data generated from your use of the App, including:</p>
          
          <h3>a) Personal Information</h3>
          <ul>
            <li>Name, email, login credentials</li>
            <li>Age, weight, height, activity level</li>
            <li>Dietary goals, preferences, and restrictions</li>
          </ul>

          <h3>b) Pantry & Meal Data</h3>
          <ul>
            <li>Ingredients you have at home</li>
            <li>Recipes you view or cook</li>
            <li>Nutrient and calorie intake logs</li>
          </ul>

          <h3>c) Usage Data</h3>
          <ul>
            <li>App usage patterns</li>
            <li>Device information (OS, version)</li>
            <li>Analytics for improving the App</li>
          </ul>
        </section>

        <section>
          <h2>2. How We Use Your Data</h2>
          <p>We use your data to:</p>
          <ol>
            <li>Provide personalized recipe suggestions and nutrient tracking</li>
            <li>Track your pantry inventory and meal history</li>
            <li>Calculate your remaining daily nutrients</li>
            <li>Improve App functionality and user experience</li>
            <li>Communicate App updates, features, or support</li>
          </ol>
          <p><strong>Legal Basis (GDPR):</strong></p>
          <ul>
            <li>Consent: You consent to data collection when using the App</li>
            <li>Contract: Data processing is necessary to provide the services you request</li>
            <li>Legitimate interest: For analytics and improving App functionality</li>
          </ul>
        </section>

        <section>
          <h2>3. Data Sharing and Disclosure</h2>
          <p>We do <strong>not sell your data</strong>.</p>
          <p>Data may be shared with:</p>
          <ul>
            <li><strong>Service providers</strong>: Cloud hosting, analytics, or app maintenance</li>
            <li><strong>Legal authorities</strong>: When required by law or regulation</li>
          </ul>
          <p>All third parties are required to protect your data in accordance with GDPR and DPA standards.</p>
        </section>

        <section>
          <h2>4. Cookies and Tracking</h2>
          <p>The App may use cookies or similar technologies to track usage for analytics and improve user experience.</p>
          <p>You can disable cookies in your device settings, but some features may be affected.</p>
        </section>

        <section>
          <h2>5. Data Retention</h2>
          <ul>
            <li>Personal and pantry data is stored <strong>only as long as necessary</strong> to provide services.</li>
            <li>You can request deletion of your account and all associated data at any time.</li>
          </ul>
        </section>

        <section>
          <h2>6. Your Rights</h2>
          <p><strong>Under GDPR (EU Users):</strong> Access, correct, delete ("right to be forgotten"), restrict processing, and data portability.</p>
          <p><strong>Under Philippine DPA (Philippine Users):</strong> Access, correct, delete/blocking, and being informed of processing.</p>
          <p><strong>How to Exercise Rights:</strong> Email martin9876543219@gmail.com with your account email and request type.</p>
        </section>

        <section>
          <h2>7. Data Security</h2>
          <p>We implement <strong>reasonable administrative, technical, and physical measures</strong> to protect your personal data.</p>
        </section>

        <section>
          <h2>8. Children’s Privacy</h2>
          <p>The App is <strong>not intended for children under 13</strong>.</p>
        </section>

        <section>
          <h2>9. Changes to this Privacy Policy</h2>
          <p>We may update this policy occasionally. Significant changes will be notified via email or in-app notification.</p>
        </section>

        <section>
          <h2>10. Contact Us</h2>
          <address>
            Email: <a href="mailto:martin9876543219@gmail.com">martin9876543219@gmail.com</a><br>
            Address: Baybay City, Leyte
          </address>
        </section>
      </article>
    </main>
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useHead, useSeoMeta } from 'nuxt/app';

const title = "LetMCook | Home";
const description =
  "Smart meal planner using your ingredients to meet nutrient goals.";

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
<style scoped></style>
<style></style>
