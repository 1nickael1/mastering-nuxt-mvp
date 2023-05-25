<template>
    <div class="p-12 bg-gray-100 w-full gap-2 min-h-screen flex">
        <div class="rounded-md w-[25ch] flex gap-2 flex-col bg-red-300 flex-grow p-2">
            <NuxtLink to="/dashboard/profile">
                Profile
            </NuxtLink>
            <NuxtLink to="/dashboard/orders">
                Orders
            </NuxtLink>
        </div>
        <div class="rounded-md w-[65ch] flex-grow">
            <NuxtPage />
        </div>
    </div>
</template>