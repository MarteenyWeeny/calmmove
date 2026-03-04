<script setup lang="ts">

const title = "Calm Move | Home";
const description = "Smart Pantry";

useSeoMeta({
    title: () => title,
    description: () => description,
    charset: "utf-8",
    viewport: "width=device-width, initial-scale=1.0"
});

useHead({
    link: [
        { rel: 'icon', type: 'image/png', href: '/logo.png' },
        { rel: 'stylesheet', href: '/reset.css' }
    ]
});
</script>

<template>
    <client-only>
        <NavBar />
        <Welcome />
        <Copyright />
    </client-only>
</template>

<style scoped></style>
<style></style>
