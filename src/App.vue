<script setup lang="ts">
import { ref } from 'vue';
import DialogConfirmDelete from './components/DialogConfirmDelete.vue';
import { DotsVerticalIcon } from '@heroicons/vue/solid';
import { Popover, PopoverButton, PopoverPanel } from '@headlessui/vue'

let dialogOpen = ref(false);
</script>

<template>
  <DialogConfirmDelete :is-open="dialogOpen" @closed="dialogOpen = false" @confirmed="dialogOpen = false">

  </DialogConfirmDelete>

  <Popover>
    <PopoverButton class="focus:outline-none cursor-pointer">
      <DotsVerticalIcon class="w-6 h-6" />
    </PopoverButton>
    <PopoverPanel class="absolute z-10">
      <div class="flex flex-col shadow-xl rounded border border-gray-200 p-4 space-y-2 bg-white">
        <span @click="dialogOpen = true">Open dialog</span>
      </div>
    </PopoverPanel>
  </Popover>
  <span @click="dialogOpen = true">Open dialog</span>
</template>