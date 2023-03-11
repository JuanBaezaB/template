<script setup>

import { Bars4Icon, ClockIcon, HomeIcon } from '@heroicons/vue/24/outline'
import { Link } from '@inertiajs/vue3';
import ApplicationMark from '@/Components/ApplicationMark.vue';


</script>
<template><!-- Sidebar -->
    <div id="sidebar" class="fixed inset-0 z-40 flex ">
        <div
            class="relative flex w-full flex-1 flex-col pt-0 pb-5 transition-colors duration-500 bg-white dark:bg-gray-800 border-slate-200 lg:border-slate-900/10 dark:border-slate-50/[0.06] border-r shadow-sm dark:shadow-none">

            <!-- Header Sidebar -->
            <header>
                <div class="flex items-center justify-between px-4">
                    <div class="flex flex-shrink-0 items-center h-16 -mb-px">
                        <Link :href="route('dashboard')">
                        <ApplicationMark class="block h-9 w-auto" />
                        </Link>
                    </div>
                    <div class="flex items-center justify-center ">
                        <button @click="sidebarClose"
                            class="inline-flex items-center justify-center w-8 h-8 mr-2 text-slate-500 transition-colors duration-150   hover:bg-slate-200 rounded-full focus:shadow-outline "
                            data-toggle="layout" data-action="sidebar_close" id="sidebar_close">
                            <svg fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"
                                xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                        </button>
                    </div>
                </div>
            </header>


            <!-- Sidebar content -->
            <div class="mt-5 h-0 flex-1 overflow-y-auto">
                <nav class="md:px-2  px-5">
                    <div class="space-y-1 ">

                        <slot/>
                    </div>

                </nav>
            </div>
        </div>

    </div>
</template>

<script>

export default {
    data() {
        return {
            pageContent: null,
            lResize: false
        }
    },
    created() {
        window.addEventListener("resize", this.resizeHandler);
    },
    destroyed() {
        window.removeEventListener("resize", this.resizeHandler);
    },

    mounted() {
        this.pageContent = document.getElementById('page-container').classList;
        this.sidebarcloseMd();

    },
    methods: {
        sidebarClose() {
            let withPage = window.innerWidth;
            if (withPage < 768) {
                this.pageContent.remove('sidebar-o-xs')
                if (this.pageContent.contains('sidebar-o-md')) {
                    this.pageContent.remove('sidebar-o-md')
                }
            } else if (withPage > 767 && withPage < 1024) {
                this.pageContent.remove('sidebar-o-md')
                if (this.pageContent.contains('sidebar-o-xs')) {
                    this.pageContent.remove('sidebar-o-xs');
                }
            }

            console.log(this.pageContent);

        },
        resizeHandler(e) {
            clearTimeout(this.lResize);
            this.pageContent.remove('side-trans-enabled')
            let page = this.pageContent;
            this.lResize = setTimeout(function (pageContent = page) {
                let withPage = window.innerWidth;
                if (withPage > 767 && withPage < 1024) {
                    if (pageContent.contains('sidebar-o-xs')) {
                        pageContent.add('sidebar-o-md');
                    }
                }
                if (withPage < 768) {
                    if (pageContent.contains('sidebar-o-md')) {
                        pageContent.add('sidebar-o-xs')
                    }
                }
                pageContent.add('side-trans-enabled')
                console.log(withPage)
            }, 500);
        },
        sidebarcloseMd() {
            const overlay = document.querySelector("#sidenav-overlay");
            const pageContent = this.pageContent;

            overlay.addEventListener('click', function (event) {
                console.log(pageContent);
                pageContent.remove('sidebar-o-md');
                if (pageContent.contains('sidebar-o-xs')) {
                    pageContent.remove('sidebar-o-xs');
                }
            });

        },

    }
}
</script>
