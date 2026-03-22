<template>
  <div id="CMLoginBox" class="CM-login-box CM-hidden">
    <div class="CM-login-header">Login</div>
    <div class="CM-login-slogan">Welcome back to CalmMove</div>

    <div id="CMLogInForm" class="CM-login-form">
      <input
        id="CMLoginUsername"
        class="CM-login-input"
        type="text"
        placeholder="Username"
      />
      <input
        id="CMLoginPassword"
        class="CM-login-input"
        type="password"
        placeholder="Password"
      />
    </div>

    <div id="CMLogInMessage" class="CM-login-message CM-hidden"></div>

    <div id="CMLogInActions" class="CM-login-actions">
      <div id="CMLoginOK" class="CM-login-action CM-login-ok" data-busy="0">
        Sign In
      </div>
    </div>
  </div>
</template>

<style scoped></style>
