<script setup lang="ts">
import { ref } from "vue";
import ReportTab from "./ReportTab.vue";

const range = ref<"daily" | "weekly" | "monthly">("daily");
</script>

<template>
  <main class="flex w-full flex-col">
    <ReportTab :range @update="(r) => (range = r)" />
  </main>
</template>
