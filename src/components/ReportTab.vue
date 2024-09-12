<script setup lang="ts">
import jeremy from "../assets/image-jeremy.png";

defineProps<{
  range: "daily" | "weekly" | "monthly";
}>();

defineEmits<{
  update: [range: "daily" | "weekly" | "monthly"];
}>();
</script>

<template>
  <div class="flex flex-col rounded-2xl bg-neutral-dark-blue">
    <div
      class="flex flex-row items-center gap-5 rounded-2xl bg-primary-blue p-8"
    >
      <img :src="jeremy.src" class="size-16 rounded-full ring-2 ring-white" />
      <div class="flex flex-col justify-center">
        <span class="text-sm text-neutral-pale-blue">Report for</span>
        <span class="text-2xl">Jeremy Robson</span>
      </div>
    </div>

    <div
      class="flex flex-row justify-between py-6 text-center text-neutral-desaturated-blue"
    >
      <span
        class="w-full cursor-pointer duration-100 hover:text-white"
        :class="{ 'text-white': range == 'daily' }"
        @click.prevent="$emit('update', 'daily')"
        >Daily</span
      >
      <span
        class="w-full cursor-pointer duration-100 hover:text-white"
        :class="{ 'text-white': range == 'weekly' }"
        @click.prevent="$emit('update', 'weekly')"
        >Weekly</span
      >
      <span
        class="w-full cursor-pointer duration-100 hover:text-white"
        :class="{ 'text-white': range == 'monthly' }"
        @click.prevent="$emit('update', 'monthly')"
        >Monthly</span
      >
    </div>
  </div>
</template>
