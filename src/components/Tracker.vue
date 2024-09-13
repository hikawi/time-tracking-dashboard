<script setup lang="ts">
import { computed, onBeforeMount, onUnmounted, ref } from "vue";
import IconEllipsis from "./icons/IconEllipsis.vue";
import IconSwitcher from "./IconSwitcher.vue";

const props = defineProps<{
  range: "daily" | "weekly" | "monthly";
  type: string;
  current: number;
  previous: number;
}>();

const lastTerm = computed(() => {
  switch (props.range) {
    case "daily":
      return "Yesterday";
    case "weekly":
      return "Last Week";
    case "monthly":
      return "Last Month";
    default:
      return "N/A";
  }
});

let color = computed(() => {
  switch (props.type) {
    case "Exercise":
      return "bg-primary-exercise";
    case "Play":
      return "bg-primary-play";
    case "Self Care":
      return "bg-primary-self-care";
    case "Social":
      return "bg-primary-social";
    case "Study":
      return "bg-primary-study";
    case "Work":
      return "bg-primary-work";
    default:
      return "bg-primary-exercise";
  }
});

// Part to check whether the window is too small
// If it's too small, show "Last" instead of "Last Week" etc.
const isTooSmall = ref(false);
function checkTooSmall() {
  isTooSmall.value = window.innerWidth < 360;
}

onBeforeMount(() => {
  checkTooSmall();
  window.addEventListener("resize", checkTooSmall);
});

onUnmounted(() => {
  window.removeEventListener("resize", checkTooSmall);
});
</script>

<template>
  <div class="flex flex-col rounded-2xl" :class="color">
    <!-- Empty height div with icon -->
    <div class="relative min-h-10 overflow-clip">
      <IconSwitcher :type class="absolute -top-2 right-4" />
    </div>

    <!-- No clue where #33367a comes from, but it's in the Figma file -->
    <div
      class="flex h-full flex-col justify-center gap-2 rounded-2xl bg-neutral-dark-blue px-6 py-7 duration-100 hover:bg-[#33367a]"
    >
      <div class="flex flex-row items-center justify-between">
        <span class="font-medium">{{ type }}</span>
        <IconEllipsis />
      </div>
      <div
        class="flex flex-row items-center justify-between lg:flex-col lg:items-start lg:justify-center lg:leading-normal"
      >
        <span class="text-[2rem] font-light lg:text-[3.5rem]"
          >{{ current }}hr{{ current == 1 ? "" : "s" }}</span
        >
        <span class="text-nowrap text-base text-neutral-pale-blue"
          >{{ isTooSmall ? "Last" : lastTerm }} - {{ previous }}hr{{
            previous == 1 ? "" : "s"
          }}</span
        >
      </div>
    </div>
  </div>
</template>
