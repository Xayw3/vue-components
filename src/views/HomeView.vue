<template>
  <AnimalsList />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AnimalsList from "@/components/AnimalsList/AnimalsList.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    AnimalsList,
  },
});
</script>
