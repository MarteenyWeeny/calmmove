<script lang="ts"></script>

<template>
  <client-only>
    <NavBar navAdminMode="" />
    <div id="CMMain" class="CM-main">
      <div class="CM-support-container">
        <h1 class="CM-support-title">Account Deletion</h1>
        <p class="CM-support-date"><strong>Effective Date:</strong> April 16, 2026</p>

        <h2 class="CM-support-section-title">Data Retention and Deletion</h2>
        <p class="CM-support-text">
          You can request the deletion of your account and all associated data at any time. When you delete your account, all your personal data and inputted information will be permanently removed from our systems.
        </p>

        <p class="CM-support-text">
          Please contact us at <a href="mailto:calmmove.support@gmail.com" class="CM-support-link">calmmove.support@gmail.com</a>.
        </p>
      </div>
    </div>
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
const title = "CalmMove | Support";
const description =
  "Support and account deletion information for CalmMove.";

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
