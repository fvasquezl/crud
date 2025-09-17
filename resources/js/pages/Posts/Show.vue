<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head } from '@inertiajs/vue3';

interface Post {
    id: number;
    title: string;
    body: string;
}

defineProps<{
    post: Post;
}
>();

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Show',
        href: '/show',
    },
];
</script>

<template>

    <Head title="Posts" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-4 overflow-x-auto rounded-xl p-4">
            <div class="flex flex-wrap flex-col">
                <h1 class="text-2xl font-bold mb-2">{{post.title}}</h1>
                <p class="text-gray-700 dark:text-gray-300 mb-4">{{post.body}}</p>
            </div>

        </div>
    </AppLayout>
</template>
