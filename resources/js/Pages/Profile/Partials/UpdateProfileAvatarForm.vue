<script setup>
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Link, useForm, usePage } from '@inertiajs/vue3';

// defineProps({
//     mustVerifyEmail: {
//         type: Boolean,
//     },
//     status: {
//         type: String,
//     },
// });

const user = usePage().props.auth.user;

const form = useForm({
    name: user.name,
    email: user.email,
});
console.log(user);
</script>

<template>
    <section>
        <header>
            <h2 class="text-lg font-medium text-gray-900 dark:text-gray-100">Profile Avatar</h2>

            <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">
                Update your account's avatar.
            </p>
        </header>

        <form @submit.prevent="form.patch(route('profile.avatar'))" class="mt-6 space-y-6">
            <div class="flex items-center gap-5">
                <InputLabel for="avatar" value="Avatar" />

                <TextInput
                    id="avatar"
                    type="file"
                    class="mt-1 block w-full"
                    v-model="form.avatar"
                    required
                    autofocus
                    autocomplete="avatar"
                />
                
                <InputError class="mt-2" :message="form.errors.avatar" />

                <div v-if="$page.props.flash.message" class="flex items-center gap-4">
                    <Transition
                        enter-active-class="transition ease-in-out"
                        enter-from-class="opacity-0"
                        leave-active-class="transition ease-in-out"
                        leave-to-class="opacity-0"
                    >
                        <p v-if="form.recentlySuccessful" class="text-sm text-gray-600 dark:text-gray-400">{{ $page.props.flash.message }}</p>
                    </Transition>
                </div>
            </div>

            <div class="flex items-center gap-4">
                <PrimaryButton :disabled="form.processing">Save</PrimaryButton>

                <Transition
                    enter-active-class="transition ease-in-out"
                    enter-from-class="opacity-0"
                    leave-active-class="transition ease-in-out"
                    leave-to-class="opacity-0"
                >
                    <p v-if="form.recentlySuccessful" class="text-sm text-gray-600 dark:text-gray-400">saved.</p>
                </Transition>
            </div>
        </form>
    </section>
</template>
