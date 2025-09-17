<script setup lang="ts">
import PostController from '@/actions/App/Http/Controllers/PostController';
import type { Post } from '@/types';
import { Form } from '@inertiajs/vue3';
import { Button } from '@/components/ui/button';
import {
    Dialog,
    DialogClose,
    DialogContent,
    DialogDescription,
    DialogFooter,
    DialogHeader,
    DialogTitle,
    DialogTrigger,
} from '@/components/ui/dialog';
import Icon from '@/components/Icon.vue';

interface Props {
    post: Post;
}

const props = defineProps<Props>();
</script>

<template>
    <Dialog>
        <DialogTrigger as-child>
            <Button variant="ghost" size="sm" class="text-red-600 hover:text-red-800 dark:text-red-400 dark:hover:text-red-300">
                <Icon name="trash2" class="h-3.5 w-3.5" />
                <span class="sr-only">Delete</span>
            </Button>
        </DialogTrigger>

        <DialogContent class="sm:max-w-md">
            <Form
                v-bind="PostController.destroy.form(props.post.id)"
                reset-on-success
                :options="{ preserveScroll: true }"
                v-slot="{ processing, reset, clearErrors }"
            >
                <DialogHeader>
                    <DialogTitle class="flex items-center gap-2 text-red-600">
                        <Icon name="alert-triangle" class="h-5 w-5" />
                        Delete Post
                    </DialogTitle>
                    <DialogDescription class="text-left">
                        Are you sure you want to delete "<strong>{{ props.post.title }}</strong>"?
                        <br><br>
                        This action cannot be undone and will permanently remove the post and all its data.
                    </DialogDescription>
                </DialogHeader>

                <DialogFooter class="gap-2 sm:gap-2">
                    <DialogClose as-child>
                        <Button
                            variant="outline"
                            @click="() => {
                                clearErrors();
                                reset();
                            }"
                        >
                            Cancel
                        </Button>
                    </DialogClose>
                    <Button
                        type="submit"
                        variant="destructive"
                        :disabled="processing"
                        class="gap-2"
                    >
                        <Icon name="trash2" class="h-4 w-4" />
                        {{ processing ? 'Deleting...' : 'Delete Post' }}
                    </Button>
                </DialogFooter>
            </Form>
        </DialogContent>
    </Dialog>
</template>