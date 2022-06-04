<template>
  <button @click="count++">Click me</button>
  <br /><br />
  {{ count }}
  <br /><br />
  <AnimalAdder @addAnimal="addAnimal" />
  <br /><br />
  <button @click="toggleView">
    {{ viewMode === "all" ? "Show only C" : "Show All" }}
  </button>
  <br /><br />
  <div v-for="(animal, index) in animalsView" :key="animal" class="animal">
    <h1>
      {{ animal }}
    </h1>
    <button @click="removeAnimal(index)">Delete</button>
  </div>
  <h1 v-if="loading">Loading.....</h1>
  <div v-for="{ id, name } in characters" :key="id">{{ name }}</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AnimalAdder from "@/components/AnimalAdder/AnimalAdder.vue";

type ViewMode = "all" | "only-c";

export default defineComponent({
  name: "HomeView",
  components: {
    AnimalAdder,
  },
  data: () => ({
    count: 10,
    viewMode: "all" as ViewMode,
    animals: [] as string[],
    loading: false,
    characters: [],
  }),
  created() {
    this.animals = JSON.parse(localStorage.getItem("animals") || "[]");
  },
  computed: {
    animalsView() {
      if (this.viewMode === "only-c") {
        return this.animalsStartingWithC;
      }

      return this.animals;
    },
    animalsStartingWithC() {
      return this.animals.filter((name) => name[0].toUpperCase() === "C");
    },
  },
  methods: {
    toggleView() {
      if (this.viewMode === "all") {
        this.viewMode = "only-c";
      } else {
        this.viewMode = "all";
      }
    },
    addAnimal(animal: string) {
      const newAnimals = [...this.animals];

      newAnimals.push(animal);

      this.animals = newAnimals;
    },
    removeAnimal(index: number) {
      const newAnimals = [...this.animals];

      newAnimals.splice(index, 1);

      this.animals = newAnimals;
    },
  },
  watch: {
    animals(newAnimals, oldAnimals) {
      localStorage.setItem("animals", JSON.stringify(newAnimals));
    },
  },
});
</script>
<style scoped lang="scss">
.animal {
  display: flex;
  align-items: center;
  gap: 10px;
  justify-content: center;

  h1 {
    margin: 0;
  }
}
</style>
