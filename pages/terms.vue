<script lang="ts"></script>

<template>
    <client-only>
        <NavBar />
        <div id="CMMain" class="CM-main"></div>
        <Copyright />
    </client-only>
</template>

<script setup lang="ts">

const title = "LetMCook | Home";
const description = "Smart meal planner using your ingredients to meet nutrient goals.";

useSeoMeta({
    title: () => title,
    description: () => description,
    charset: "utf-8",
    viewport: "width=device-width, initial-scale=1.0"
});

useHead({
    link: [
        {rel: 'icon', type: 'image/png', href: '/logo.png'},
        {rel: 'stylesheet', href: '/reset.css'},
        {rel: 'stylesheet', href: '/custom.css'} ,
        {rel: 'preconnect', href: 'https://fonts.googleapis.com'},
        {rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: ''},
        {rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=Funnel+Sans:ital,wght@0,300..800;1,300..800&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap'}
    ]
});

</script>
<style scoped></style>
<style></style>
