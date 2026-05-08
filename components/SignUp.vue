<template>
    <client-only>
        <div id="CMSignUpBox" class="CM-web-box bh-hidden">
            <div class="CM-web-header">Sign Up</div>
            <div class="CM-web-slogan">Make the world cleaner.</div>
            <div id="CMSignUpForm" class="CM-web-form">
                <input
                id="CMSignUpFullName"
                name="CMSignUpFullName"
                type="text"
                class="CM-web-input"
                placeholder="Full name"
                required
                />
                <input
                id="CMSignUpEmail"
                name="CMSignUpEmail"
                type="text"
                class="CM-web-input"
                placeholder="Email"
                required
                />
                <input
                id="CMSignUpPassword"
                name="CMSignUpPassword"
                type="password"
                class="CM-web-input"
                placeholder="Password"
                required
                />
            </div>
            <div id="CMSignUpMessage" class="CM-web-message CM-hidden">
            Test message...
            </div>
            <div id="CMSignUpActions" class="CM-web-actions">
                <div id="CMSignUpOK" class="CM-web-action CM-web-ok">Sign Up</div>
            </div>
        </div>
    </client-only>
</template>