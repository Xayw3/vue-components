<template>
  <AnimalSwitcher v-on:change="toggleAnimals" />
  <AnimalAdder @addAnimal="addAnimal" />
  <ul class="list" v-for="animal in animalsView" :key="animal.id">
    <li class="list-item">
      <p>{{ animal.name }}</p>
      <p>{{ animal.species }}</p>
      <button @click="removeAnimal">Delete</button>
    </li>
  </ul>
</template>

<style lang="scss">
@import "./animals-list.scss";
</style>

<script lang="ts">
import AnimalsTypes from "@/models/AnimalsModel";
import { defineComponent } from "vue";
import AnimalAdder from "@/components/AnimalAdder/AnimalAdder.vue";
import AnimalSwitcher from "../AnimalSwitcher/AnimalSwitcher.vue";

type ViewMode = "cat" | "dog";

export default defineComponent({
  name: "AnimalsList",
  components: {
    AnimalAdder,
    AnimalSwitcher,
  },
  data: () => ({
    animals: [] as AnimalsTypes[],
    viewMode: "cat" as ViewMode,
  }),
  created() {
    this.animals = JSON.parse(localStorage.getItem("animals") || "[]");
  },
  computed: {
    animalsView() {
      if (this.viewMode === "cat") {
        return this.allCats;
      }

      return this.allDogs;
    },
    allCats() {
      return this.animals.filter((el) => el.species === "cat");
    },
    allDogs() {
      return this.animals.filter((el) => el.species === "dog");
    },
  },
  methods: {
    addAnimal(animal: AnimalsTypes) {
      const newAnimals = [...this.animals];

      newAnimals.push(animal);

      console.log(newAnimals);

      this.animals = newAnimals;
    },
    removeAnimal(index: any) {
      const newAnimals = [...this.animals];

      newAnimals.splice(index, 1);

      this.animals = newAnimals;
    },
    toggleAnimals() {
      if (this.viewMode === "cat") {
        this.viewMode = "dog";
      } else {
        this.viewMode = "cat";
      }
    },
  },
  watch: {
    animals(newAnimals) {
      localStorage.setItem("animals", JSON.stringify(newAnimals));
    },
  },
});
</script>
