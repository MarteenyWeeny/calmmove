<template>
  <client-only>
    <NavBar />
    <main id="CMMain" class="CM-main">
      <article class="pp-article">
        <header class="pp-header">
          <h1 class="pp-title">Privacy Policy – LetMCook</h1>
          <p class="pp-effective-date"><strong>Effective Date:</strong> March 11, 2026</p>
        </header>

        <section class="pp-intro">
          <p>At LetMCook App, your privacy is important.</p>
          <p>This Privacy Policy explains how we collect, use, store, and protect your personal data in accordance with the <strong>EU General Data Protection Regulation (GDPR)</strong> and the <strong>Philippine Data Privacy Act of 2012 (DPA)</strong>.</p>
          <p>By using the App, you consent to the practices described here.</p>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">1. Information We Collect</h2>
          <p>We collect information you provide and data generated from your use of the App, including:</p>
          
          <h3 class="pp-subsection-title">a) Personal Information</h3>
          <ul class="pp-list">
            <li>Name, email, login credentials</li>
            <li>Age, weight, height, activity level</li>
            <li>Dietary goals, preferences, and restrictions</li>
          </ul>

          <h3 class="pp-subsection-title">b) Pantry & Meal Data</h3>
          <ul class="pp-list">
            <li>Ingredients you have at home</li>
            <li>Recipes you view or cook</li>
            <li>Nutrient and calorie intake logs</li>
          </ul>

          <h3 class="pp-subsection-title">c) Usage Data</h3>
          <ul class="pp-list">
            <li>App usage patterns</li>
            <li>Device information (OS, version)</li>
            <li>Analytics for improving the App</li>
          </ul>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">2. How We Use Your Data</h2>
          <p>We use your data to:</p>
          <ol class="pp-list pp-list--ordered">
            <li>Provide personalized recipe suggestions and nutrient tracking</li>
            <li>Track your pantry inventory and meal history</li>
            <li>Calculate your remaining daily nutrients</li>
            <li>Improve App functionality and user experience</li>
            <li>Communicate App updates, features, or support</li>
          </ol>
          <div class="pp-callout">
            <p><strong>Legal Basis (GDPR):</strong></p>
            <ul class="pp-list">
              <li>Consent: You consent to data collection when using the App</li>
              <li>Contract: Data processing is necessary to provide the services you request</li>
              <li>Legitimate interest: For analytics and improving App functionality</li>
            </ul>
          </div>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">3. Data Sharing and Disclosure</h2>
          <p>We do <strong>not sell your data</strong>.</p>
          <p>Data may be shared with:</p>
          <ul class="pp-list">
            <li><strong>Service providers</strong>: Cloud hosting, analytics, or app maintenance</li>
            <li><strong>Legal authorities</strong>: When required by law or regulation</li>
          </ul>
          <p>All third parties are required to protect your data in accordance with GDPR and DPA standards.</p>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">4. Cookies and Tracking</h2>
          <p>The App may use cookies or similar technologies to track usage for analytics and improve user experience.</p>
          <p>You can disable cookies in your device settings, but some features may be affected.</p>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">5. Data Retention</h2>
          <ul class="pp-list">
            <li>Personal and pantry data is stored <strong>only as long as necessary</strong> to provide services.</li>
            <li>You can request deletion of your account and all associated data at any time.</li>
          </ul>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">6. Your Rights</h2>
          <div class="pp-rights-grid">
            <div class="pp-rights-card">
              <h3 class="pp-subsection-title">Under GDPR (EU Users):</h3>
              <ul class="pp-list">
                <li>Access your personal data</li>
                <li>Correct inaccurate or incomplete data</li>
                <li>Request deletion ("right to be forgotten")</li>
                <li>Restrict or object to processing</li>
                <li>Data portability</li>
              </ul>
            </div>
            <div class="pp-rights-card">
              <h3 class="pp-subsection-title">Under Philippine DPA (Philippine Users):</h3>
              <ul class="pp-list">
                <li>Access your personal data</li>
                <li>Correct errors in your data</li>
                <li>Request deletion or blocking</li>
                <li>Be informed of how your data is processed</li>
              </ul>
            </div>
          </div>
          <div class="pp-callout">
            <p><strong>How to Exercise Rights:</strong> Email <a href="mailto:martin9876543219@gmail.com" class="CM-footer-links">martin9876543219@gmail.com</a> with your account email and request type.</p>
          </div>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">7. Data Security</h2>
          <p>We implement <strong>reasonable administrative, technical, and physical measures</strong> to protect your personal data.</p>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">8. Children's Privacy</h2>
          <p>The App is <strong>not intended for children under 13</strong>.</p>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">9. Changes to this Privacy Policy</h2>
          <p>We may update this policy occasionally. Significant changes will be notified via email or in-app notification.</p>
        </section>

        <section class="pp-section">
          <h2 class="pp-section-title">10. Contact Us</h2>
          <address class="pp-address">
            Email: <a href="mailto:martin9876543219@gmail.com" class="CM-footer-links">martin9876543219@gmail.com</a><br>
            Address: Baybay City, Leyte
          </address>
        </section>
      </article>
    </main>
    <Copyright />
  </client-only>
</template>

<style scoped>
.pp-article {
  max-width: 800px;
  margin: 80px auto 60px;
  padding: 0 5%;
  color: #374151;
  line-height: 1.75;
}

.pp-header {
  margin-bottom: 32px;
  padding-bottom: 16px;
  border-bottom: 2px solid #e5e7eb;
}

.pp-title {
  font-size: 2em;
  font-weight: 700;
  color: #0f766e;
  margin-bottom: 6px;
}

.pp-effective-date {
  font-size: 0.9em;
  color: #6b7280;
}

.pp-intro {
  margin-bottom: 32px;
}

.pp-intro p + p {
  margin-top: 10px;
}

.pp-section {
  margin-bottom: 40px;
}

.pp-section-title {
  font-size: 1.25em;
  font-weight: 700;
  color: #111827;
  margin-bottom: 12px;
  padding-bottom: 8px;
  border-bottom: 1px solid #e5e7eb;
}

.pp-subsection-title {
  font-size: 0.95em;
  font-weight: 600;
  color: #374151;
  margin: 16px 0 8px;
}

.pp-list {
  padding-left: 20px;
  margin: 8px 0 12px;
}

.pp-list li {
  margin-bottom: 6px;
  font-size: 0.92em;
}

.pp-list--ordered {
  list-style: decimal;
}

.pp-callout {
  margin: 16px 0;
  padding: 16px 20px;
  background-color: #f9fafb;
  border-left: 3px solid #84cc16;
  border-radius: 0 6px 6px 0;
}

.pp-rights-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  margin-bottom: 16px;
}

.pp-rights-card {
  padding: 16px;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
  background-color: #ffffff;
}

.pp-address {
  font-style: normal;
  font-size: 0.92em;
  line-height: 2;
}

@media (max-width: 640px) {
  .pp-rights-grid {
    grid-template-columns: 1fr;
  }
}
</style>