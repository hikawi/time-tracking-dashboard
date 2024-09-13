<script setup lang="ts">
import IconExercise from "./icons/IconExercise.vue";
import IconPlay from "./icons/IconPlay.vue";
import IconSelfCare from "./icons/IconSelfCare.vue";
import IconSocial from "./icons/IconSocial.vue";
import IconStudy from "./icons/IconStudy.vue";
import IconWork from "./icons/IconWork.vue";

defineProps<{
  type: string;
}>();
</script>

<template>
  <IconExercise v-if="type === 'Exercise'" />
  <IconPlay v-else-if="type === 'Play'" />
  <IconSelfCare v-else-if="type === 'Self Care'" />
  <IconSocial v-else-if="type === 'Social'" />
  <IconStudy v-else-if="type === 'Study'" />
  <IconWork v-else />
</template>
