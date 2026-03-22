<script lang="ts"></script>
<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="CMMain" class="CM-main">
      <Login />
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
const router = useRouter();
let navAdminMode = userLevel.value >= 2 ? "CM-nav-admin" : "";
const CMServer = "https://calmmove-api.vercel.app";
type AuthResponse = {
  accessToken: string;
  userLevel: number;
  fullName: string;
  message: string;
};
function getByID<T extends HTMLElement>(id: string) {
  return document.getElementById(id) as T;
}
let lastLoginClicked = 0;
function checkAuthorizations() {
  if (accessToken.value) {
    if (userLevel.value <= 1) {
      router.push("/");
    } else if (userLevel.value >= 2) {
      router.push("/admin");
    }
  }
  const loginBox = getByID<HTMLDivElement>("CMLoginBox");
  const loginForm = getByID<HTMLDivElement>("CMLogInForm");
  const loginUsername = getByID<HTMLInputElement>("CMLoginUsername");
  const loginPassword = getByID<HTMLInputElement>("CMLoginPassword");
  const loginMessage = getByID<HTMLDivElement>("CMLogInMessage");
  const logInActions = getByID<HTMLDivElement>("CMLogInActions");
  const loginOK = getByID<HTMLDivElement>("CMLoginOK");
  if (
    !loginBox ||
    !loginForm ||
    !loginUsername ||
    !loginPassword ||
    !loginMessage ||
    !logInActions ||
    !loginOK
  )
    return;
  if (retries.value >= 3) {
    loginForm.classList.add("CM-hidden");
    loginMessage.classList.remove("CM-hidden");
    loginMessage.innerText = "Too many attempts, try again after 1 hour.";
    logInActions.classList.add("CM-hidden");
    return;
  }
  loginOK.dataset.busy = "0";
  loginBox.classList.remove("CM-hidden");
  loginOK.addEventListener("click", () => {
    if (loginOK.dataset.busy == "1") return;
    const tempUsername = loginUsername.value;
    const tempPassword = loginPassword.value;
    if (!tempUsername) {
      loginMessage.innerText = "Username is required.";
      loginMessage.classList.remove("CM-hidden");
      return;
    }
    if (!tempPassword) {
      loginMessage.innerText = "Password is required.";
      loginMessage.classList.remove("CM-hidden");
      return;
    }
    authorizeEmail(tempUsername, tempPassword);
  });
  loginUsername.addEventListener("keyup", (e) => {
    if (e.key === "Enter" && loginUsername.value) {
      loginPassword.focus();
    }
  });
  loginPassword.addEventListener("keyup", (e) => {
    if (e.key === "Enter") loginOK.click();
  });
  loadModal();
}
async function authorizeEmail(tempUsername: string, tempPassword: string) {
  if (lastLoginClicked >= Date.now() - globalDelay) return;
  lastLoginClicked = Date.now();
  const loginUsername = getByID<HTMLInputElement>("CMLoginUsername");
  const loginPassword = getByID<HTMLInputElement>("CMLoginPassword");
  const loginMessage = getByID<HTMLDivElement>("CMLogInMessage");
  const loginOK = getByID<HTMLDivElement>("CMLoginOK");
  if (!loginUsername || !loginPassword || !loginOK || !loginMessage) return;
  loginMessage.innerText = "";
  loginMessage.classList.add("CM-hidden");
  loginUsername.disabled = true;
  loginPassword.disabled = true;
  loginOK.dataset.busy = "1";
  try {
    userLevel.value = -1;
    const response = (await $fetch(`${CMServer}/authorize`, {
      headers: { "Content-Type": "application/json" },
      method: "POST",
      body: {
        username: tempUsername,
        password: tempPassword,
      },
    })) as AuthResponse;
    accessToken.value = String(response.accessToken);
    userLevel.value = Number(response.userLevel);
    fullName.value = String(response.fullName);
    if (accessToken.value) {
      username.value = tempUsername;
    }
    loginOK.dataset.busy = "0";
    if (!accessToken.value) {
      retries.value = (retries.value || 0) + 1;
    }
    if (response.message) {
      loginMessage.innerText = response.message;
      loginMessage.classList.remove("CM-hidden");
    }
  } catch (e: any) {
    loginMessage.innerText = `Error encountered: ${e}`;
    loginMessage.classList.remove("CM-hidden");
  }
  loginUsername.disabled = false;
  loginPassword.disabled = false;
  loginUsername.value = "";
  loginPassword.value = "";
  loginOK.dataset.busy = "0";
  checkAuthorizations();
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
}
onMounted(() => {
  nextTick(checkAuthorizations);
});
</script>
<style>
.CM-login-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  padding: 20px;
  background: #fff;
  border-radius: 8px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 0 1px #000000bf;
}
.CM-login-header {
  font-size: 1.3em;
  font-weight: bold;
  text-align: center;
  line-height: 2em;
}
.CM-login-slogan {
  margin: 10px 0 20px 0;
  text-align: center;
}
.CM-login-form {
  margin-top: 20px;
}
.CM-login-input {
  margin-bottom: 10px;
  padding: 8px 10px;
  width: 100%;
  font-size: 1.1em;
  border-radius: 3px;
  border: 1px solid rgba(0, 0, 0, 0.3);
  outline: none;
}
.CM-login-message {
  padding: 8px;
  font-size: 0.7em;
  background-color: rgba(255, 0, 0, 0.1);
  border: 1px solid rgba(255, 0, 0, 0.3);
  border-radius: 3px;
}
.CM-login-actions {
  margin-top: 20px;
}
.CM-login-action {
  padding: 10px;
  text-align: center;
  border-radius: 6px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  cursor: pointer;
}
.CM-login-ok {
  color: #fff;
  background-color: #3f7d58;
}
.CM-login-ok:hover {
  color: #fff;
  background-color: #3f7d58dd;
}
</style>
