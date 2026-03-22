<template>
  <client-only>
    <header :class="['CM-navbar', navAdminMode]">
      <nav class="CM-nav-left">
        <a href="/" class="CM-nav-home">
          <img src="/logo.png" width="20" height="20" class="CM-nav-logo" />
          <span>CalmMove</span>
        </a>
      </nav>
      <nav id="CMNavBasic" class="CM-nav-right CM-hidden">
        <ul>
          <li><a href="#" class="CM-nav-link">Recipes</a></li>
          <li><a href="#" class="CM-nav-link">Pantry</a></li>
          <li><a href="#" class="CM-nav-link">Tracker</a></li>
          <li><span id="CMNavBasicLogout" class="CM-nav-link">Logout</span></li>
        </ul>
      </nav>
      <nav id="CMNavAdmin" class="CM-nav-right CM-hidden">
        <ul>
          <li><a href="#" class="CM-nav-link">Settings</a></li>
          <li><a href="#" class="CM-nav-link">Reports</a></li>
          <li><span id="CMNavAdminLogout" class="CM-nav-link">Logout</span></li>
        </ul>
      </nav>
    </header>
  </client-only>
</template>
<script setup lang="ts">
const props = defineProps<{ navAdminMode: string }>();
</script>
