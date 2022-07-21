<script setup lang="ts">
import {
    Dialog,
    DialogPanel,
    DialogTitle,
    TransitionChild,
    TransitionRoot,
} from "@headlessui/vue";
import XIcon from "@heroicons/vue/solid/XIcon";

const props = defineProps<{
    isOpen: boolean;
}>();

const emit = defineEmits(["closed", "confirmed"]);

</script>

<template>
    <TransitionRoot appear :show="isOpen" as="template">
        <Dialog as="div" @close="$emit('closed')" class="relative z-10">
            <TransitionChild as="template" enter="duration-300 ease-out" enter-from="opacity-0" enter-to="opacity-100"
                leave="duration-200 ease-in" leave-from="opacity-100" leave-to="opacity-0">
                <div class="fixed inset-0 bg-black bg-opacity-25" />
            </TransitionChild>

            <div class="fixed inset-0 overflow-y-auto">
                <div class="flex min-h-full items-center justify-center p-4 text-center">
                    <TransitionChild as="template" enter="duration-300 ease-out" enter-from="opacity-0 scale-95"
                        enter-to="opacity-100 scale-100" leave="duration-200 ease-in" leave-from="opacity-100 scale-100"
                        leave-to="opacity-0 scale-95">
                        <DialogPanel
                            class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white p-6 text-left align-middle shadow-xl transition-all">
                            <DialogTitle as="h3"
                                class="text-lg font-medium leading-6 text-gray-900 flex justify-between items-center">
                                <span class="font-semibold">Bevestigen?</span>
                                <XIcon class="cursor-pointer w-8 h-8 p-1 hover:bg-gray-200 rounded"
                                    @click="$emit('closed')" />
                            </DialogTitle>
                            <div class="mt-2">
                                <p class="text-sm leading-5 text-gray-900">
                                    <slot name="text">
                                        Are you sure you want to delete this item?
                                    </slot>
                                </p>
                                <div class="w-full border-b border-gray-300 my-2"></div>
                                <div class="flex flex-row space-x-2">
                                    <button class="bg-red-200 text-red-900 px-2 py-1 rounded"
                                        @click="$emit('confirmed')">Delete</button>
                                    <button class="border border-slate-300 text-slate-500 rounded px-2 py-1"
                                        @click="$emit('closed')">Cancel</button>
                                </div>
                            </div>
                        </DialogPanel>
                    </TransitionChild>
                </div>
            </div>
        </Dialog>
    </TransitionRoot>
</template>