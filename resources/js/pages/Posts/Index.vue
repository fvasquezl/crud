<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, Link } from '@inertiajs/vue3';
import { create} from '@/routes/posts';
import { Button } from '@/components/ui/button';
import Icon from '@/components/Icon.vue';
import type { Post } from '@/types';
import ListPostActions from '@/components/Posts/ListPostActions.vue';

defineProps<{
    posts: Post[];
}
>();

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Posts',
        href: '/posts',
    },
];
</script>

<template>

    <Head title="Posts" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-6 overflow-x-auto rounded-xl p-6">
            <!-- Header Section -->
            <div class="flex flex-col gap-4 sm:flex-row sm:items-center sm:justify-between">
                <div>
                    <h1 class="text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Posts</h1>
                    <p class="mt-2 text-sm text-gray-600 dark:text-gray-400">Manage your blog posts and articles.</p>
                </div>
                <Button as-child>
                    <Link :href="create()" class="inline-flex items-center gap-2">
                        <Icon name="plus" class="h-4 w-4" />
                        New Post
                    </Link>
                </Button>
            </div>

            <!-- Table Container -->
            <div class="bg-white dark:bg-gray-900 shadow-sm ring-1 ring-gray-900/5 dark:ring-white/10 rounded-lg overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-800">
                        <thead class="bg-gray-50 dark:bg-gray-800/50">
                            <tr>
                                <th scope="col" class="px-6 py-4 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                    <div class="flex items-center gap-2">
                                        <Icon name="hash" class="h-3 w-3" />
                                        ID
                                    </div>
                                </th>
                                <th scope="col" class="px-6 py-4 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                    <div class="flex items-center gap-2">
                                        <Icon name="file-text" class="h-3 w-3" />
                                        Title
                                    </div>
                                </th>
                                <th scope="col" class="px-6 py-4 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                    <div class="flex items-center gap-2">
                                        <Icon name="align-left" class="h-3 w-3" />
                                        Content
                                    </div>
                                </th>
                                <th scope="col" class="px-6 py-4 text-right text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                    Actions
                                </th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-gray-200 dark:divide-gray-800 bg-white dark:bg-gray-900">
                            <tr v-for="post in posts" :key="post.id"
                                class="hover:bg-gray-50 dark:hover:bg-gray-800/50 transition-colors duration-200">
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <div class="flex items-center">
                                        <span class="inline-flex items-center justify-center h-8  rounded-full bg-blue-100 dark:bg-blue-900/20 text-blue-800 dark:text-blue-300 text-sm font-medium">
                                            {{ post.id }}
                                        </span>
                                    </div>
                                </td>
                                <td class="px-6 py-4">
                                    <div class="flex flex-col">
                                        <div class="text-sm font-medium text-gray-900 dark:text-white max-w-xs truncate">
                                            {{ post.title }}
                                        </div>
                                    </div>
                                </td>
                                <td class="px-6 py-4">
                                    <div class="text-sm text-gray-600 dark:text-gray-400 max-w-md">
                                        <p class="line-clamp-2">{{ post.body }}</p>
                                    </div>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                                    <div class="flex items-center justify-end gap-2">
                                        <ListPostActions :post="post" />
                                    </div>
                                </td>
                            </tr>
                        </tbody>
                    </table>

                    <!-- Empty State -->
                    <div v-if="posts.length === 0" class="text-center py-12">
                        <Icon name="file-text" class="h-12 w-12 text-gray-400 dark:text-gray-600 mx-auto mb-4" />
                        <h3 class="text-sm font-medium text-gray-900 dark:text-white">No posts yet</h3>
                        <p class="mt-1 text-sm text-gray-500 dark:text-gray-400">Get started by creating your first post.</p>
                        <div class="mt-6">
                            <Button as-child>
                                <Link :href="create()" class="inline-flex items-center gap-2">
                                    <Icon name="plus" class="h-4 w-4" />
                                    New Post
                                </Link>
                            </Button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
