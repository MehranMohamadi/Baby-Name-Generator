<template>

  <div class="option-container">
    <h4>{{ props.option.title }}</h4>
    <div class="options-buttons">
      <button
          v-for="value in option.buttons " :key="value"
          class="option option-left"
          :class=" options[option.category] === value && 'option-active'"
          @click="options[option.category]=value">
        {{ value }}

      </button>

    </div>
  </div>
</template>

<script setup lang="ts">
import {Gender, Length, Popularity} from "~/data";

interface OptionsProps {
  option: {
    title: string;
    category: string;
    buttons: Gender[] | Popularity[] | Length[]
  };
  options: {
    gender: Gender;
    popularity: Popularity;
    length: Length
  }
}

const props = defineProps<OptionsProps>()


</script>

<style scoped>

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  position: relative;

}

.option-container {
  margin-bottom: 2rem;

}

.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;

}

.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-left {
  border-radius: 1rem 0 0 1rem;

}

.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}
</style>