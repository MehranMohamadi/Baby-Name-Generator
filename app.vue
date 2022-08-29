<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <P>Choose youre option and click "find names"</P>
    <div class="options-container">
     <Option v-for="option in optionsArray"
             :key="option.title" :option="option" :options="options" />
      <button class="primary" @click="computedSelectednames">Find Name</button>
    </div>
    <div class="cards-container">
      <div v-for="name in selectedNames" :key="name" class="card">

        <h4> {{ name }}</h4>
        <p>x</p>
      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
import {Gender, Length, names, Popularity} from './data'
import Option from "~/components/Option.vue";



interface OptionState {
  gender: Gender;
  popularity: Popularity;
  length: Length
}

const Options: OptionState = reactive(
    {
      gender: Gender.GIRL,
      length: Length.LONG,
      popularity: Popularity.UNIQUE
    });

const computedSelectednames = () => {
  const filterNames = names.filter((name) => name.gender === Options.gender)
      .filter((name) => name.popularity === Options.popularity)
      .filter((name) => {
        if (Options.length === Length.ALL) return true;
        else return name.length === options.length
      })

  selectedNames.value = filterNames.map((name) => name.name)
}
const selectedNames = ref<string[]>([])

const optionsArray = [
  {
    title: "1) choose a gender",
    category: 'gender',
    buttons: [Gender.GIRL, Gender.UNISEX, Gender.BOY],
  },
  {
    title: "1) choose a names popularity",
    category: 'popularity',
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "1) choose the names length",
    category: 'length',
    buttons: [Length.SHORT, Length.ALL, Length.LONG],
  }
]
</script>


<style scoped>
.container {
  font-family: Arial, serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

.container h1 {
  font-size: 3rem;

}


.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
  border: none;

}


.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}

.card {
  background-color: rgb(27, 61, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
}

.card p {
  position: absolute;
  top: -30%;
  left: 92.5%;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.178);

}
</style>