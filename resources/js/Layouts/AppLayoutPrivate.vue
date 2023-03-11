<script setup>
import { ref } from 'vue';
import { Head, Link, router } from '@inertiajs/vue3';
import AppHeader from '../Components/Layouts/Header.vue';
import AppSidebar from '../Components/Layouts/Sidebar.vue';

import ApplicationMark from '@/Components/ApplicationMark.vue';
import Banner from '@/Components/Banner.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/Layouts/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';

import { ChartBarIcon } from '@heroicons/vue/24/outline'
defineProps({
    title: String,
});

const showingNavigationDropdown = ref(false);

const logout = () => {
    router.post(route('logout'));
};
</script>

<template>
    <Head :title="title" />


    <div id="page-container" class="sidebar-o side-trans-enabled min-h-full transition-page-all duration-200 ease-in-out">
        <div id="sidenav-overlay"></div>

        <AppSidebar>

            <NavLink :href="route('dashboard')" :active="route().current('dashboard')"
                class="group flex items-center px-2 py-2 text-base leading-5 font-medium rounded-md">
                <ChartBarIcon class="mr-3 flex-shrink-0 h-5 w-5" />
                Dashboard
            </NavLink>

        </AppSidebar>


        <div class="flex flex-col">
            <AppHeader>
                <div class="flex items-center">
                    <!-- Settings Dropdown -->
                    <div class="ml-3 relative">
                        <Dropdown align="right" width="48">
                            <template #trigger>
                                <button v-if="$page.props.jetstream.managesProfilePhotos"
                                    class="flex text-sm justify-center items-center group dark:text-gray-100 text-slate-700">
                                    <img class="h-8 w-8 rounded-full object-cover" :src="$page.props.user.profile_photo_url"
                                        :alt="$page.props.user.name">
                                    <div class="flex items-center truncate">
                                        <span class="truncate ml-2 text-sm font-medium">
                                            {{ $page.props.user.name }}
                                        </span>
                                        <svg class="w-3 h-3 shrink-0 ml-3 fill-current text-slate-400" viewBox="0 0 12 12">
                                            <path d="M5.9 11.4L.5 6l1.4-1.4 4 4 4-4L11.3 6z"></path>
                                        </svg>
                                    </div>
                                </button>

                            </template>
                            <template #content >
                                <!-- Account Management -->
                                <div class="block px-4 py-2 text-xs text-gray-400">
                                    Manage Account
                                </div>

                                <DropdownLink :href="route('profile.show')">
                                    Profile
                                </DropdownLink>

                                <div class="border-t border-gray-100 dark:border-slate-50/[0.06] " />

                                <!-- Authentication -->
                                <form @submit.prevent="logout">
                                    <DropdownLink as="button">
                                        Log Out
                                    </DropdownLink>
                                </form>
                            </template>
                        </Dropdown>
                    </div>
                </div>
            </AppHeader>

            <header v-if="$slots.header" class="transition-colors duration-500 bg-white dark:bg-gray-700 shadow">
                <div class="max-w-7xl mx-auto py-10 px-4 sm:px-6 lg:px-8">
                    <slot name="header" />
                </div>
            </header>

            <transition name="page" mode="out-in" appear>
                <main id="main-panel" :key="$page.url">
                    <slot />
                </main>
            </transition>
        </div>



    </div>
</template>


<style>
.page-enter-active,
.page-leave-active {
    transition: opacity 1s ease;
}

.page-enter-from,
.page-leave-to {
    opacity: 0;
}
</style>
