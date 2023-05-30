<template>
    <div class="flex-col">
        <p>Hello world</p>
        <hr class="my-2">
        <div class="flex gap-2 underline">
            <NuxtLink to="/course">Course</NuxtLink>
            <NuxtLink :href="firstLesson.path">Go to first lesson</NuxtLink>
            <NuxtLink to="/dashboard">Dashboard</NuxtLink>
            <NuxtLink to="/login">Login</NuxtLink>
        </div>
        <div class="flex flex-col underline gap-2">
            <NuxtLink to="/teste1">Pagina de produto 1</NuxtLink>
            <NuxtLink to="/teste2">Pagina de produto 2</NuxtLink>
            <NuxtLink to="/teste3">Pagina de categoria 1</NuxtLink>
            <NuxtLink to="/teste4">Pagina de categoria 2</NuxtLink>
        </div>
    </div>
</template>

<script setup lang="ts">
const firstLesson = await useFirstLesson();

</script>