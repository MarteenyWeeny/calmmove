<script lang="ts"></script>
<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="CMMain" class="CM-main">
      <span id="CMPageTitle" class="CM-page-title CM-hidden">Latest</span>
      <div id="CMContainer" class="CM-container"></div>
    </div>
    <Cookies />
    <Copyright />
  </client-only>
</template>
<script setup lang="ts">
const title = "CalmMove";
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
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Funnel+Sans:ital,wght@0,300..800;1,300..800&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap",
    },
  ],
});
const globalDelay = 500;
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
type ContentItem = {
  id: string;
  author: string;
  title: string;
  content: string;
  isSynchronized: number;
  createdAt: number;
};
type ContentResponse = {
  contents: ContentItem[];
};
const router = useRouter();
const CMServer = "https://calmmove-api.vercel.app";
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
  loadModal();
}
function loadModal() {
  const cookieModal = getByID<HTMLDivElement>("CMCookieModal");
  const cookieBox = getByID<HTMLDivElement>("CMCookieBox");
  const cookieX = getByID<HTMLDivElement>("CMCookieX");
  const cookieOK = getByID<HTMLDivElement>("CMCookieOK");
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
function showCookiePopup(show: boolean = true) {
  const cookieBox = getByID<HTMLDivElement>("CMCookieBox");
  const cookieModal = getByID<HTMLDivElement>("CMCookieModal");
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
function allowAllCookies() {
  if (lastCookieClicked >= Date.now() - globalDelay) return;
  lastCookieClicked = Date.now();
  allowCookies.value = true;
  showCookiePopup(false);
  loadContents();
}
onMounted(() => {
  nextTick(() => {
    checkAuthorizations();
  });
});
async function loadContents() {
  if (!accessToken.value) return;
  var rawContents = [] as ContentItem[];
  try {
    const query = new URLSearchParams({
      username: username.value,
      userLevel: String(userLevel.value),
      accessToken: accessToken.value,
    }).toString();
    const response = (await $fetch(`${CMServer}/get_contents?${query}`, {
      headers: { "Content-Type": "application/json" },
      method: "GET",
    })) as ContentResponse;
    rawContents = response.contents;
  } catch (e: any) {
    return;
  }
  const container = getByID<HTMLDivElement>("CMContainer");
  if (!container) return;
  container.innerHTML = "";
  const contents = renderContents(rawContents) as HTMLElement;
  container.appendChild(contents);
}
function renderContents(data: ContentItem[]): HTMLElement {
  const parent = document.createElement("div");
  parent.className = "CM-contents";
  data.forEach((item, index) => {
    const wrapper = document.createElement("div");
    wrapper.id = `content-${index}`;
    wrapper.className = "CM-content-box";
    const title = document.createElement("h2");
    title.className = "CM-content-title";
    title.textContent = item.title;
    const meta = document.createElement("p");
    const date = new Date(item.createdAt * 1000);
    const published = date.toLocaleDateString("en-US", {
      year: "numeric",
      month: "long",
      day: "numeric",
    });
    meta.textContent = `by ${item.author} • ${published}`;
    meta.className = "CM-content-meta";
    const content = document.createElement("p");
    content.className = "CM-content-data";
    content.textContent = item.content;
    wrapper.append(title, meta, content);
    parent.appendChild(wrapper);
  });
  return parent;
}
</script>