<script setup>
import AppLayout from '@/Layouts/AppLayoutPrivate.vue';
import Welcome from '@/Components/Welcome.vue';
import { ChevronLeftIcon, ChevronRightIcon, HomeIcon } from '@heroicons/vue/20/solid'

const pages = [
    { name: 'Projects', href: '#', current: false },
    { name: 'Project Nero', href: '#', current: true },
]
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <div>
                <div>
                    <nav class="flex" aria-label="Breadcrumb">
                        <ol role="list" class="flex items-center space-x-4">
                            <li>
                                <div class="flex items-center">
                                    <a href="#" class="text-gray-400 hover:text-gray-500">
                                        <HomeIcon class="h-5 w-5 flex-shrink-0" aria-hidden="true" />
                                        <span class="sr-only">Home</span>
                                    </a>
                                </div>
                            </li>
                            <li v-for="page in pages" :key="page.name">
                                <div class="flex items-center">
                                    <ChevronRightIcon class="h-5 w-5 flex-shrink-0 text-gray-400" aria-hidden="true" />
                                    <a :href="page.href" class="ml-4 text-sm font-medium text-gray-500 hover:text-gray-700"
                                        :aria-current="page.current ? 'page' : undefined">{{ page.name }}</a>
                                </div>
                            </li>
                        </ol>
                    </nav>
                </div>

                <div class="mt-3 md:flex md:items-center md:justify-between">
                    <div class="min-w-0 flex-1">
                        <h2
                            class="text-2xl font-bold leading-7 transition-colors duration-500 text-gray-800 dark:text-gray-100 sm:truncate sm:text-3xl sm:tracking-tight">
                            Dashboard</h2>
                    </div>
                </div>
            </div>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <Welcome />
                </div>
            </div>
        </div>
    </AppLayout>
</template>
