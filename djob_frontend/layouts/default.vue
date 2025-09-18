<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

function logout() {
    userStore.removeToken()
}
</script>

<template>
    <div class="flex flex-col min-h-screen">
        <!-- Navbar -->
        <nav class="bg-teal-900 text-white">
        <div class="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
            <NuxtLink to="/" class="text-2xl font-semibold">Djob</NuxtLink>

            <div class="flex items-center space-x-6">
            <NuxtLink to="/" class="hover:text-teal-300">Home</NuxtLink>
            <NuxtLink to="/browse" class="hover:text-teal-300">Browse</NuxtLink>

            <template v-if="userStore.user.isAuthenticated">
                <NuxtLink to="/myjobs" class="hover:text-teal-300">My Jobs</NuxtLink>
                <NuxtLink to="/createjob" class="hover:text-teal-300">Create Job</NuxtLink>
                <button
                @click="logout"
                class="ml-4 px-4 py-2 bg-rose-600 hover:bg-rose-700 rounded text-white text-sm"
                >
                Logout
                </button>
            </template>
            <template v-else>
                <NuxtLink
                to="/login"
                class="px-4 py-2 bg-teal-600 hover:bg-teal-700 rounded text-white text-sm"
                >
                Log in
                </NuxtLink>
                <NuxtLink
                to="/signup"
                class="px-4 py-2 bg-teal-600 hover:bg-teal-700 rounded text-white text-sm"
                >
                Sign up
                </NuxtLink>
            </template>
            </div>
        </div>
        </nav>

        <!-- Page Content -->
        <main class="flex-1">
        <slot />
        </main>

        <!-- Footer -->
        <footer class="bg-gray-900 text-gray-400">
        <div class="max-w-6xl mx-auto px-6 py-6 flex flex-col md:flex-row items-center justify-between">
            <p class="text-sm">&copy; 2023 Djob. All rights reserved.</p>
            <p class="text-sm mt-2 md:mt-0">Built with Nuxt3 + Django REST</p>
        </div>
        </footer>
    </div>
</template>
