<template>
  <div>
    <form class="form" @submit.prevent="submitHandler">
      <input
        class="input"
        type="text"
        placeholder="Add new animal...."
        v-model="inputValue"
      />
      <select class="input" v-model="selectValue" name="animal">
        <option hidden value="">Select value</option>
        <option value="dog">Dog</option>
        <option value="cat">Cat</option>
      </select>
      <button class="btn-primary btn" type="submit">Add animal</button>
    </form>
  </div>
</template>

<style lang="scss">
@import "./animal-adder.scss";
</style>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "AnimalAdder",
  emits: ["addAnimal"],
  data() {
    return {
      inputValue: "",
      selectValue: "",
      id: 0,
    };
  },
  methods: {
    submitHandler() {
      this.$emit("addAnimal", {
        name: this.inputValue,
        species: this.selectValue,
        id: (this.id += 1),
      });

      this.inputValue = "";
    },
  },
});
</script>
