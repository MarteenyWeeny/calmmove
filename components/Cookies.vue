<template>
    <client-only>
        <div id="CMCookieModal" class="CM-cookie-modal CM-hidden"></div>
        <div id="CMCookieBox" class="CM-cookie-box CM-hidden">
            <span id="CMCookieX" class="CM-cookie-x">✕</span>
            <div class="CM-cookie-header" >Cookies and Privacy</div>
            <div class="CM-cookie-message">
                We use cookies to ensure you get the best experience on our website.
            </div>
            <div class="CM-cookie-actions">
                <a href="/policy" class="CM-cookie-link" target="_blank">
                    <div class="CM-cookie-action CM-cookie-more">Read more</div>
                </a>
                <div id="CMCookieOK" class="CM-cookie-action CM-cookie-ok">Accept all</div>
            </div>
        </div>
    </client-only>
</template>
