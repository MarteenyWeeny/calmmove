<template>
  <client-only>
    <div id="CMSignInBox" class="CM-web-box CM-hidden">
      <div class="CM-web-header">Sign In</div>
      <div class="CM-web-slogan">Make the world cleaner.</div>
      <div id="CMSignInForm" class="CM-web-form">
        <input
          id="CMSignInEmail"
          name="CMSignInEmail"
          type="text"
          class="CM-web-input"
          placeholder="Email"
          required
        />
        <input
          id="CMSignInPassword"
          name="CMSignInPassword"
          type="password"
          class="CM-web-input"
          placeholder="Password"
          required
        />
      </div>
      <div id="CMSignInMessage" class="CM-web-message CM-hidden">
        Test message...
      </div>
      <div id="CMSignInActions" class="CM-web-actions">
        <div id="CMSignInOK" class="CM-web-action CM-web-ok">Sign In</div>
      </div>
    </div>
  </client-only>
</template>