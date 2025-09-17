<script setup lang="ts">
import PostController from '@/actions/App/Http/Controllers/PostController';
import { Input } from '@/components/ui/input';
import { Form } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Button } from '@/components/ui/button';
import Label from '@/components/ui/label/Label.vue';
import TextArea from '@/components/ui/textarea/TextArea.vue';
import { computed } from 'vue';
import type { Post } from '@/types';

// More specific types based on mode
interface CreateProps {
    mode: 'create';
    post?: never;
}

interface EditProps {
    mode: 'edit';
    post: Post;
}

type Props = CreateProps | EditProps;

const props = defineProps<Props>();

// Determine the form configuration based on mode
const formConfig = computed(() => {
    if (props.mode === 'edit') {
        return PostController.update.form(props.post.id);
    }
    return PostController.store.form();
});

// Button text based on mode
const submitText = computed(() => {
    return props.mode === 'create' ? 'Create Post' : 'Update Post';
});

// Reset fields based on mode
const resetFields = computed(() => {
    return ['title', 'body'];
});
</script>

<template>
    <Form
        v-bind="formConfig"
        :reset-on-success="resetFields"
        v-slot="{ errors, processing, recentlySuccessful }"
        class="flex flex-col gap-6"
    >
        <div class="grid gap-6">
            <div class="grid gap-2">
                <Label for="title">Title</Label>
                <Input
                    id="title"
                    type="text"
                    autofocus
                    autocomplete="title"
                    name="title"
                    placeholder="Enter post title"
                    :model-value="props.mode === 'edit' ? props.post.title : ''"
                />
                <InputError :message="errors.title" />
            </div>

            <div class="grid gap-2">
                <Label for="body">Content</Label>
                <TextArea
                    id="body"
                    name="body"
                    placeholder="Write your post content here..."
                    :rows="6"
                    :model-value="props.mode === 'edit' ? props.post.body : ''"
                />
                <InputError :message="errors.body" />
            </div>

            <div class="flex items-center gap-4">
                <Button :disabled="processing" type="submit">
                    {{ processing ? (mode === 'create' ? 'Creating...' : 'Updating...') : submitText }}
                </Button>

                <Transition
                    enter-active-class="transition ease-in-out"
                    enter-from-class="opacity-0"
                    leave-active-class="transition ease-in-out"
                    leave-to-class="opacity-0"
                >
                    <p v-show="recentlySuccessful" class="text-sm text-emerald-600 dark:text-emerald-400">
                        {{ mode === 'create' ? 'Post created successfully!' : 'Post updated successfully!' }}
                    </p>
                </Transition>
            </div>
        </div>
    </Form>
</template>