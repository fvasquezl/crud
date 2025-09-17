<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head } from '@inertiajs/vue3';
import PostForm from '@/components/Posts/PostForm.vue';
import type { Post } from '@/types';

defineProps<{
    post: Post;
}>();

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Posts',
        href: '/posts',
    },
    {
        title: 'Edit',
        href: '/posts/edit',
    },
];
</script>

<template>
    <Head :title="`Edit Post - ${post.title}`" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-6 overflow-x-auto rounded-xl p-6">
            <div class="flex flex-col gap-2">
                <h1 class="text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Edit Post</h1>
                <p class="text-sm text-gray-600 dark:text-gray-400">Update the details of your blog post.</p>
            </div>

            <div class="bg-white dark:bg-gray-900 shadow-sm ring-1 ring-gray-900/5 dark:ring-white/10 rounded-lg p-6">
                <PostForm mode="edit" :post="post" />
            </div>
        </div>
    </AppLayout>
</template>