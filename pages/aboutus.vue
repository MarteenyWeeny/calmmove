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
                <span class="person-name">Person 1</span>
                <span class="person-role">Project Manager</span>
              </div>
              <div class="person">
                <span class="person-name">Person 2</span>
                <span class="person-role">Database Designer</span>
              </div>
              <div class="person">
                <span class="person-name">Person 3</span>
                <span class="person-role">Web Designer</span>
              </div>
              <div class="person-ellipsis">...</div>
              <div class="person">
                <span class="person-name">Person 6</span>
                <span class="person-role">Backend Developer</span>
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
<style>
.CM-nav-link:hover {
  cursor: pointer;
}
.CM-page-title {
  position: relative;
  margin: 60px auto 0;
  width: 800px;
  max-width: 90%;
  padding: 20px;
  font-size: 1.8em;
  font-weight: bold;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  display: block;
}
.CM-container {
  position: relative;
  margin: 20px auto 0;
  width: 800px;
  max-width: 90%;
}
.CM-content-box {
  margin-bottom: 10px;
  padding: 20px;
  background: #fff;
  border-radius: 3px;
  border: 1px solid rgba(0, 0, 0, 0.2);
}
.CM-content-title {
  line-height: 1.5em;
  font-weight: bold;
}
.CM-content-meta {
  font-size: 0.8em;
  color: #666;
  margin-bottom: 20px;
}
/* Team specific styles */
.about-team {
  margin-top: 20px;
}
.person {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 15px;
  margin-bottom: 8px;
  background: #f9f9f9;
  border-radius: 6px;
}
.person-name {
  font-size: 1.1em;
  font-weight: 500;
  color: #333;
}
.person-role {
  font-size: 0.9em;
  color: #666;
  background: #e8f5e9;
  padding: 4px 12px;
  border-radius: 20px;
}
.person-ellipsis {
  text-align: center;
  font-size: 1.3em;
  color: #999;
  margin: 5px 0;
}
</style>