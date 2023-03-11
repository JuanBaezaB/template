<script setup>

import DarkModeToggle from './DarkModeToggle.vue'
</script>

<template>
    <!-- Content Header -->
    <header id="page-header"
        class="sticky top-0  w-full flex-none transition-colors duration-500 lg:z-50 border-b border-slate-900/10 dark:border-slate-50/[0.06] bg-white/95 dark:bg-gray-800 shadow-none">
        <div class="px-4 sm:px-6 lg:px-16">
            <div class="flex items-center justify-between h-16 -mb-px">

                <div class="flex">
                    <button @click="SidebarToggle"
                        class="text-slate-500 dark:hover:text-white  hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 rounded-lg text-sm p-1 inline-flex items-center dark:text-gray-400   dark:hover:bg-gray-700 dark:focus:ring-gray-600"
                        aria-controls="sidebar" id="sidebar_toggle" aria-expanded="false">
                        <span class="sr-only">
                            Open sidebar
                        </span>
                        <svg class="w-7 h-7" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"
                            xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                            <path class="fill-current " stroke-linecap="round" stroke-linejoin="round"
                                d="M3.75 6.75h16.5M3.75 12H12m-8.25 5.25h16.5"></path>
                        </svg>
                    </button>
                </div>

                <div class="flex items-center gap-1">


                    <div class="relative inline-flex border-r transition-colors duration-500 border-slate-200 mr-3 pr-3 dark:border-slate-600">
                        <DarkModeToggle />
                    </div>


                    <slot/>

                </div>
            </div>
        </div>
    </header>

</template>

<script>


export default {
    data() {
        return {
            pageContent: null
        }
    },

    mounted() {
        this.pageContent = document.getElementById('page-container').classList;
    },
    methods: {
        SidebarToggle() {
            let withPage = window.innerWidth;
            if (withPage > 1023) {
                this.pageContent.toggle('sidebar-o')
                if (this.pageContent.contains('sidebar-o-md')) {
                    this.pageContent.remove('sidebar-o-md')
                }
                if (this.pageContent.contains('sidebar-o-xs')) {
                    this.pageContent.remove('sidebar-o-xs')
                }


            } else if (withPage > 767 && withPage < 1024) {
                this.pageContent.toggle('sidebar-o-md')
                if (this.pageContent.contains('sidebar-o-xs')) {
                    this.pageContent.remove('sidebar-o-xs')
                }
                console.log(withPage)

            } else if (withPage < 768) {
                this.pageContent.toggle('sidebar-o-xs')
            }


        }
    }
}
</script>
