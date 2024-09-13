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
  <div class="flex flex-col rounded-2xl bg-neutral-dark-blue lg:row-span-2">
    <div
      class="flex flex-row items-center gap-5 rounded-2xl bg-primary-blue p-8 lg:flex-col lg:items-start lg:gap-10"
    >
      <img
        :src="jeremy.src"
        alt="Jeremy Robson"
        class="size-16 rounded-full ring-2 ring-white lg:size-20 lg:ring-4"
      />
      <div class="flex flex-col justify-center">
        <span class="text-sm text-neutral-pale-blue">Report for</span>
        <h1 class="text-2xl font-light leading-tight lg:mb-12 lg:text-[2.5rem]">
          Jeremy Robson
        </h1>
      </div>
    </div>

    <div
      class="flex flex-row justify-between py-6 text-center text-neutral-desaturated-blue lg:flex-col lg:gap-5 lg:px-8 lg:text-left"
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
