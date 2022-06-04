<template>
  <div class="form-check form-switch">
    <label class="form-check-label" for="flexSwitchCheckDefault"
      >{{ checked }}
      <input
        class="form-check-input"
        type="checkbox"
        id="flexSwitchCheckDefault"
        v-on:change="changeValue"
      />
    </label>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "AnimalSwitcher",
  data() {
    return {
      checked: "Show cats",
    };
  },
  methods: {
    changeValue() {
      if (this.checked === "Show cats") {
        this.checked = "Show dogs";
      } else {
        this.checked = "Show cats";
      }
    },
  },
});
</script>
