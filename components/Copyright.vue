<script setup lang="ts">
const year = new Date().getFullYear();
</script>

<template>
  <client-only>
    <footer class="CM-footer-area">
      <nav class="CM-footer-links">
        <a href="/terms">Terms of Service</a>
        <span>&nbsp;|&nbsp;</span>
        <a href="/policy">Privacy Policy</a>
        <span>&nbsp;|&nbsp;</span>
        <a href="support">Support</a>
      </nav>
      <div class="CM-footer-copyright">
        <span>&copy;&nbsp;</span>
        <span>{{ year }}</span>
        <span>&nbsp;LetMCook. All rights reserved.</span>
      </div>
    </footer>
  </client-only>
</template>
