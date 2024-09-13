<script setup lang="ts">
import { ref } from "vue";
import ReportTab from "./ReportTab.vue";
import data from "../assets/data.json";
import Tracker from "./Tracker.vue";

const range = ref<"daily" | "weekly" | "monthly">("weekly");
const items = ref(data);

function shuffleArray(array: any[]) {
  for (let i = array.length - 1; i >= 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
}

function randomize() {
  const copy = [...items.value];
  shuffleArray(copy);
  items.value = copy;
}
</script>

<template>
  <main
    class="flex w-full flex-col gap-6 text-lg md:w-1/2 lg:grid lg:w-full lg:grid-flow-row lg:grid-cols-4 lg:grid-rows-2 xl:w-4/5"
  >
    <ReportTab :range @update="(r) => (range = r)" />
    <Tracker
      v-for="item in items"
      :current="item.timeframes[range].current"
      :previous="item.timeframes[range].previous"
      :type="item.title"
      :key="item.title"
      :range
    />

    <button
      class="fixed bottom-4 left-1/2 hidden min-w-fit -translate-x-1/2 rounded-2xl bg-primary-blue px-5 py-2 text-sm duration-100 hover:bg-neutral-desaturated-blue lg:block"
      @click="randomize"
    >
      Randomize slots
    </button>
  </main>
</template>
