<template>
    <client-only>
        <NavBar :navAdminMode="navAdminMode" />
        <div id="CMMain" class="CM-main"></div>
        <Cookies />
        <Copyright />
    </client-only>
</template>

<script setup lang="ts">
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
    href:
"https://fonts.googleapis.com/css2?family=Funnel+Sans:ital,wght@0,300..800;1,300..800&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap",
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

const router = useRouter();
const navAdminMode = computed(() =>
    userLevel.value >= 2 ? "CM-nav-admin" : "",
);

function getByID<T extends HTMLElement>(id: string) {
    return document.getElementById(id) as T;
}

function checkAuthorizations() {
    if (userLevel.value === -1) {
        if (router.currentRoute.value.path !== "/") {
            router.push("/");
        }
        return;
    } else if (userLevel.value >= 2) {
        router.push("/admin");
    }

    const navGuest = getByID<HTMLDivElement>("CMNavGuest");
    const navBasic = getByID<HTMLDivElement>("CMNavBasic");
    const navAdmin = getByID<HTMLDivElement>("CMNavAdmin");
    const navLogout = getByID<HTMLDivElement>("CMNavBasicLogout");
    const pageTitle = getByID<HTMLSpanElement>("CMPageTitle");

    if (!navGuest || !navBasic || !navAdmin || !navLogout || !pageTitle) return;

    navLogout.addEventListener("click", () => {
        emailAddress.value = "";
        accessToken.value = "";
        userLevel.value = -1;
        fullName.value = "";
        
        router.push("/signin");
    });
    navGuest.remove();
    navAdmin.remove();
    navBasic.classList.remove("CM-hidden");
    pageTitle.classList.remove("CM-hidden");

    loadModal();
}

function loadModal() {
    const cookieModal = getByID<HTMLDivElement>("CMCookieModal");
    const cookieX = getByID<HTMLDivElement>("CMCookieX");
    const cookieOK = getByID<HTMLDivElement>("CMCookieOK");
    if (!cookieModal || !cookieX || !cookieOK) return;

    if (allowCookies.value) {
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

onMounted(async () => {
    await nextTick();
    checkAuthorizations();
});
</script>