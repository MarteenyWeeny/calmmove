<!-- pages/about.vue -->
<script lang="ts"></script>
<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="CMMain" class="CM-main">
      <span id="CMPageTitle" class="CM-page-title">About Us</span>
      <div id="CMContainer" class="CM-container">
        <div class="CM-contents">
          <div class="CM-content-box">
            <h2 class="CM-content-title">Our Team</h2>
            <p class="CM-content-meta">Meet the people behind CalmMove</p>
            <div class="about-team">

              <div class="person">
                <img class="person-avatar" src="/ybas.png" alt="Martin Benedict E. Ybas profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/ybas">Martin Benedict E. Ybas</NuxtLink>
                  <span class="person-role">Project Manager</span>
                  <p class="person-desc">Motivated CS student with a strong background in competitive programming, algorithms, hackathons, and quantum computing.</p>
                </div>
              </div>

              <div class="person">
                <img class="person-avatar" src="/gvega.png" alt="Geryme Vega profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/gvega">Geryme Vega</NuxtLink>
                  <span class="person-role">Backend Developer</span>
                  <p class="person-desc">DOST-SEI Scholar and competitive programmer focused on algorithms, data structures, and efficient low-level C++ solutions.</p>
                </div>
              </div>

              <div class="person">
                <img class="person-avatar" src="/ppiangco.jpg" alt="Pete Alexander Piangco profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/ppiangco">Pete Alexander Piangco</NuxtLink>
                  <span class="person-role">Backend Developer</span>
                  <p class="person-desc">Builds high-impact software with a foundation in system design and algorithms, focused on fast and reliable experiences.</p>
                </div>
              </div>

              <div class="person">
                <img class="person-avatar" src="/kahano.jpg" alt="John Andrei B. Kahano profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/kahano">John Andrei B. Kahano</NuxtLink>
                  <span class="person-role">Database Designer</span>
                  <p class="person-desc">Fuses mathematical logic with software design to create immersive, high-performance digital frontiers.</p>
                </div>
              </div>

              <div class="person">
                <img class="person-avatar" src="/rmoreno.jpg" alt="Radz Ponce A. Moreno profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/rmoreno">Radz Ponce A. Moreno</NuxtLink>
                  <span class="person-role">Web Designer</span>
                  <p class="person-desc">Builds software that turns ideas into impact through web development, algorithms, and system design.</p>
                </div>
              </div>

              <div class="person">
                <img class="person-avatar" src="/lmcaduyac.png" alt="Liza Mae Caduyac profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/lmcaduyac">Liza Mae Caduyac</NuxtLink>
                  <span class="person-role">Web Designer</span>
                  <p class="person-desc">Passionate about seamless user experiences, efficient backend solutions, and modern web frameworks.</p>
                </div>
              </div>

              <div class="person">
                <img class="person-avatar" src="/euloPic.jpg" alt="Eulo Rod M. Coting profile picture">
                <div class="person-content">
                  <NuxtLink class="person-name" to="/ecoting">Eulo Rod M. Coting</NuxtLink>
                  <span class="person-role">Web Designer</span>
                  <p class="person-desc">Aspiring web designer and frontend developer passionate about visually stunning, user-friendly websites.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Cookies />
    <Copyright />
  </client-only>
</template>
<script setup lang="ts">
const title = "About Us - CalmMove";
const description = "Meet the team behind CalmMove.";
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
const allowCookies = useCookie<boolean>("allowCookies", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
allowCookies.value = allowCookies.value ?? false;
const retries = useCookie<number>("retries", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60,
});
retries.value = retries.value ?? 0;
const username = useCookie<string>("username", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
username.value = username.value ?? "";
const accessToken = useCookie<string>("accessToken", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
accessToken.value = accessToken.value ?? "";
const userLevel = useCookie<number>("userLevel", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
userLevel.value = userLevel.value ?? -1;
const fullName = useCookie<string>("fullName", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
fullName.value = fullName.value ?? "";
const router = useRouter();
let navAdminMode = userLevel.value >= 2 ? "CM-nav-admin" : "";
function getByID<T extends HTMLElement>(id: string) {
  return document.getElementById(id) as T;
}
function checkAuthorizations() {
  if (!accessToken.value) {
    router.push("/login");
  } else if (userLevel.value >= 2) {
    router.push("/admin");
  }
  const navBasic = getByID<HTMLDivElement>("CMNavBasic");
  const navAdmin = getByID<HTMLDivElement>("CMNavAdmin");
  const navLogout = getByID<HTMLDivElement>("CMNavBasicLogout");
  const pageTitle = getByID<HTMLSpanElement>("CMPageTitle");
  if (!navBasic || !navAdmin || !navLogout || !pageTitle) return;
  navLogout.addEventListener("click", (e) => {
    retries.value = 0;
    username.value = "";
    accessToken.value = "";
    userLevel.value = -1;
    fullName.value = "";
    router.push("/login");
  });
  navAdmin.remove();
  navBasic.classList.remove("CM-hidden");
  pageTitle.classList.remove("CM-hidden");
}
onMounted(() => {
  nextTick(() => {
    checkAuthorizations();
  });
});
</script>