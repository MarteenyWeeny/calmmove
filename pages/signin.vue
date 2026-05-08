<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="CMMain" class="CM-main">
      <SignIn />
    </div>
    <Cookies />
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";

const title = "CalmMove";
const description = "Smart meal planner using your ingredients to meet nutrient goals.";

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
const cookieOptions = {
  sameSite: "none" as const,
  secure: true,
  maxAge: 60 * 60 * 24,
};

const allowCookies = useCookie<boolean>("allowCookies", cookieOptions);
allowCookies.value = allowCookies.value ?? false;

const emailAddress = useCookie<string>("emailAddress", cookieOptions);
emailAddress.value = emailAddress.value ?? "";

const accessToken = useCookie<string>("accessToken", cookieOptions);
accessToken.value = accessToken.value ?? "";

const userLevel = useCookie<number>("userLevel", cookieOptions);
userLevel.value = userLevel.value ?? -1;

const fullName = useCookie<string>("fullName", cookieOptions);
fullName.value = fullName.value ?? "";

let lastSignInClicked = 0;
const router = useRouter();
const navAdminMode = computed(() =>
  userLevel.value >= 2 ? "CM-nav-admin" : "",
);

// ONLY POTENTIAL PLACEHOLDER: Verify this matches your team's Vercel backend.
const CMServer = "https://calmmove-api.vercel.app";

type AuthResponse = {
  success: number;
  accessToken: string;
  userLevel: number;
  message: string;
};

function getByID<T extends HTMLElement>(id: string) {
  return document.getElementById(id) as T | null;
}

function checkAuthorizations() {
  if (accessToken.value) {
    if (userLevel.value <= 1) {
      router.push("/");
    } else if (userLevel.value >= 2) {
      router.push("/admin");
    }
  }

  const signinBox = getByID<HTMLDivElement>("CMSignInBox");
  const signinEmail = getByID<HTMLInputElement>("CMSignInEmail");
  const signinPassword = getByID<HTMLInputElement>("CMSignInPassword");
  const signinMessage = getByID<HTMLDivElement>("CMSignInMessage");
  const signinOK = getByID<HTMLDivElement>("CMSignInOK");

  if (
    !signinBox ||
    !signinEmail ||
    !signinPassword ||
    !signinMessage ||
    !signinOK
  )
    return;

  signinBox.classList.remove("CM-hidden");

  signinOK.addEventListener("click", () => {
    if (signinOK.dataset.busy == "1") return;

    const tempEmail = signinEmail.value;
    const tempPassword = signinPassword.value;

    if (!tempEmail) {
      signinMessage.innerText = "Email is required.";
      signinMessage.classList.remove("CM-hidden");
      return;
    }

    if (!tempPassword) {
      signinMessage.innerText = "Password is required.";
      signinMessage.classList.remove("CM-hidden");
      return;
    }

    signInWithPassword(tempEmail, tempPassword);
  });

  signinEmail.addEventListener("keyup", (e) => {
    if (e.key === "Enter" && signinEmail.value) {
      signinPassword.focus();
    }
  });

  signinPassword.addEventListener("keyup", (e) => {
    if (e.key === "Enter") signinOK.click();
  });

  loadModal();
}

async function signInWithPassword(tempEmail: string, tempPassword: string) {
  if (lastSignInClicked >= Date.now() - globalDelay) return;
  lastSignInClicked = Date.now();

  const signinEmail = getByID<HTMLInputElement>("CMSignInEmail");
  const signinPassword = getByID<HTMLInputElement>("CMSignInPassword");
  const signinMessage = getByID<HTMLDivElement>("CMSignInMessage");
  const signinOK = getByID<HTMLDivElement>("CMSignInOK");

  if (!signinEmail || !signinPassword || !signinOK || !signinMessage) return;

  let isSuccessful = false;
  signinMessage.innerText = "";
  signinMessage.classList.add("CM-hidden");
  [signinEmail, signinPassword].forEach((el) => (el.disabled = true));
  signinOK.dataset.busy = "1";

  try {
    const response = (await $fetch(`${CMServer}/signin`, {
      headers: { "Content-Type": "application/json" },
      method: "POST",
      body: {
        email: tempEmail,
        password: tempPassword
      },
    })) as AuthResponse;

    isSuccessful = Boolean(response.success === 1);
    emailAddress.value = tempEmail;
    accessToken.value = response.accessToken;
    userLevel.value = response.userLevel;

    if (response.message) {
      signinMessage.innerText = response.message;
      signinMessage.classList.remove("CM-hidden");
    }
  } catch (e: any) {
    signinMessage.innerText = `Error encountered: ${e}`;
    signinMessage.classList.remove("CM-hidden");
  } finally {
    signinOK.dataset.busy = "0";
  }

  [signinEmail, signinPassword].forEach((el) => {
    el.remove();
  });
  signinOK.dataset.busy = "0";

  if (isSuccessful) {
    router.push("/");
  }
}

function loadModal() {
  const cookieX = getByID<HTMLDivElement>("CMCookieX");
  const cookieOK = getByID<HTMLDivElement>("CMCookieOK");
  if (!cookieX || !cookieOK) return;

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
  if (!cookieBox || !cookieModal) return;

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
}

onMounted(() => {
  nextTick(checkAuthorizations);
});
</script>