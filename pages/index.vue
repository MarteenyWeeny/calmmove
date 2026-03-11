<script setup lang="ts">
const globalDelay = 500;

const allowCookies = useCookie<boolean>("allowCookies", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});

allowCookies.value = allowCookies.value || false;

async function loadModal() {
  const cookieModal = document.getElementById("CMCookieModal") as HTMLDivElement;
  const cookieBox = document.getElementById("CMCookieBox") as HTMLDivElement;
  const cookieX = document.getElementById("CMCookieX") as HTMLDivElement;
  const cookieOK = document.getElementById("CMCookieOK") as HTMLDivElement;

  if (!cookieModal || !cookieBox || !cookieX || !cookieOK) return;

  if (allowCookies.value === true) {
    allowAllCookies();
    return;
  }

  showCookiePopup();

  cookieX.addEventListener("click", () => {
    showCookiePopup(false);
  });

  cookieOK.addEventListener("click", () => {
    allowAllCookies();
  });
}

async function showCookiePopup(show: boolean = true) {
  const cookieBox = document.getElementById("CMCookieBox") as HTMLDivElement;
  const cookieModal = document.getElementById("CMCookieModal") as HTMLDivElement;

  if (!cookieBox || !cookieModal) {
    setTimeout(showCookiePopup, 50);
    return;
  }

  if (!show) {
    cookieBox.classList.add("CM-hidden");
    cookieModal.classList.add("CM-hidden");
    return;
  }

  cookieBox.classList.remove("CM-hidden");
  cookieModal.classList.remove("CM-hidden");
}

let lastCookieClicked = 0;

async function allowAllCookies() {
  if (lastCookieClicked >= Date.now() - globalDelay) return;
  lastCookieClicked = Date.now();

  allowCookies.value = true;
  showCookiePopup(false);
}

onMounted(() => {
  setTimeout(() => {
    loadModal();
  }, 1);
});

/* Index Page */

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
    {
      rel: "preconnect",
      href: "https://fonts.gstatic.com",
      crossorigin: "",
    },
    {
      rel: "stylesheet",
      href:
        "https://fonts.googleapis.com/css2?family=Funnel+Sans:ital,wght@0,300..800;1,300..800&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap",
    },
  ],
});
</script>

<template>
  <client-only>
    <NavBar />
    <div id="CMMain" class="CM-main"></div>
    <Cookies />
    <Copyright />
  </client-only>
</template>

<style scoped></style>
<style></style>
