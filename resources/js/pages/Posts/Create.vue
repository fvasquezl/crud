<script setup lang="ts">
import PostController from '@/actions/App/Http/Controllers/PostController';
import { Input } from '@/components/ui/input';
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Form, Head } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Button } from '@/components/ui/button';
import Label from '@/components/ui/label/Label.vue';
import TextArea from '@/components/ui/textarea/TextArea.vue';



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
            <Form v-bind="PostController.store.form()" :reset-on-success="['title', 'body']"
                v-slot="{ errors, processing,recentlySuccessful }" class="flex flex-col gap-6">
                <div class="grid gap-6">
                    <div class="grid gap-2">
                        <Label for="title">Title</Label>
                        <Input id="title" type="text" autofocus :tabindex="1" autocomplete="title" name="title"
                            placeholder="Title" />
                        <InputError :message="errors.title" />
                    </div>

                    <div class="grid gap-2">
                        <Label for="body">Body</Label>
                        <TextArea id="body" name="body" placeholder="Body" :rows="3" />
                        <InputError :message="errors.body" />
                    </div>

                    <div class="flex items-center gap-4">
                        <Button :disabled="processing" data-test="update-profile-button">Save</Button>

                        <Transition enter-active-class="transition ease-in-out" enter-from-class="opacity-0"
                            leave-active-class="transition ease-in-out" leave-to-class="opacity-0">
                            <p v-show="recentlySuccessful" class="text-sm text-neutral-600">Saved.</p>
                        </Transition>
                    </div>
                </div>
            </Form>
        </div>
    </AppLayout>
</template>
