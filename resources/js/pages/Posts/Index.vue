<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, Link } from '@inertiajs/vue3';
import { create } from '@/routes/posts';


interface Post {
    id: number;
    title: string;
    body: string;
}

defineProps<{
    posts: Post[];
}
>();

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Posts',
        href: 'posts',
    },
];
</script>

<template>

    <Head title="Posts" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-4 overflow-x-auto rounded-xl p-4">
            <div class="px-4 sm:px-6 lg:px-8">
                <div class="sm:flex sm:items-center">
                    <div class="sm:flex-auto">
                        <h1 class="text-base font-semibold text-gray-900 dark:text-white">Posts</h1>
                        <p class="mt-2 text-sm text-gray-700 dark:text-gray-300">List of posts.</p>
                    </div>
                    <div class="mt-4 sm:mt-0 sm:ml-16 sm:flex-none">
                        <Link :href="create()"
                            class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 dark:bg-indigo-500 dark:hover:bg-indigo-400 dark:focus-visible:outline-indigo-500">
                        Add post
                        </Link>
                    </div>
                </div>
                <div class="mt-8 flow-root">
                    <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
                            <table class="min-w-full divide-y divide-gray-300 dark:divide-white/15">
                                <thead>
                                    <tr class="divide-x divide-gray-200 dark:divide-white/10">
                                        <th scope="col"
                                            class="py-3.5 pr-4 pl-4 text-left text-sm font-semibold text-gray-900 sm:pl-0 dark:text-white">
                                            ID
                                        </th>
                                        <th scope="col"
                                            class="px-4 py-3.5 text-left text-sm font-semibold text-gray-900 dark:text-white">
                                            Title</th>
                                        <th scope="col"
                                            class="px-4 py-3.5 text-left text-sm font-semibold text-gray-900 dark:text-white">
                                            Body</th>
                                        <th scope="col"
                                            class="py-3.5 pr-4 pl-4 text-left text-sm font-semibold text-gray-900 sm:pr-0 dark:text-white">
                                            Actions
                                        </th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-gray-200 bg-white dark:divide-white/10 dark:bg-gray-900">
                                    <tr v-for="post in posts" :key="post.id"  class="divide-x divide-gray-200 dark:divide-white/10">
                                        <td
                                            class="py-4 pr-4 pl-4 text-sm font-medium whitespace-nowrap text-gray-900 sm:pl-0 dark:text-white">
                                            {{post.id}}
                                        </td>
                                        <td class="p-4 text-sm whitespace-nowrap text-gray-500 dark:text-gray-300">{{post.title}}</td>
                                        <td class="p-4 text-sm whitespace-nowrap text-gray-500 dark:text-gray-300">{{post.body}}</td>
                                        <td
                                            class="py-4 pr-4 pl-4 text-sm whitespace-nowrap text-gray-500 sm:pr-0 dark:text-gray-300">
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
