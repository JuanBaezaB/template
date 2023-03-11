<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    href: String,
    active: Boolean,
});

const classes = computed(() => {
    return props.active
        ? 'dark:bg-gray-900 bg-gray-100 dark:text-gray-100 text-gray-900'
        : 'text-gray-600 hover:text-gray-900 dark:text-gray-400 dark:hover:text-gray-100 hover:bg-gray-100 dark:hover:bg-gray-900';
});
</script>

<template>
    <Link :href="href" :class="classes">
        <slot />
    </Link>
</template>
