<script setup>
import { ref } from 'vue';
import SingleCard from './components/SingleCard.vue';
import SwotInput from './components/SwotInput.vue';
// import {itemsStrengths, itemsWeaknesses, itemsOpportunities, itemsThreats } from './components/SwotInput.vue'

const swotAnalysisObjective = ref('');
function displayBtnIdOnInput(header){
  console.log(header)
  
  swotAnalysisObjective.value = header;
  console.log('id ' + swotAnalysisObjective.value)
};

const itemsStrengths = ref([
  {id:1, label:"cup of tea"},
  {id:2, label:"nice book"},
  {id:3, label:"black jacket"}
]);
const itemsWeaknesses = ref([
  {id:1, label:"10 of us"},
  {id:2, label:"one two three"},
  {id:3, label:"1 of 10"}
]);
const itemsOpportunities = ref([
  {id:1, label:"cup of coffe"},
  {id:2, label:"a piece of cake"},
  {id:3, label:"who is bob?"}
]);
const itemsThreats = ref([
  {id:1, label:"go for a walk"},
  {id:2, label:"run Forest run"},
  {id:3, label:"singing in the rain"}
]);

defineProps({
  itemsStrengths:{
    type: Object
  },
  itemsWeaknesses:{
    type: Object
  },
  itemsOpportunities:{
    type: Object
  },
  itemsThreats:{
    type: Object
  },
})

const addItemToSwotList = (swotObjective, addedSwotElement) => {
  console.log(addedSwotElement)
  console.log(swotObjective)
  const newItem = { id: Date.now(), label: addedSwotElement }; // Using Date.now() for unique ID
  console.log(newItem)
  switch(swotObjective) {
    case 'Strengths':
      itemsStrengths.value.push(newItem);
      break;
    case 'Weaknesses':
      itemsWeaknesses.value.push(newItem);
      break;
    case 'Opportunities':
      itemsOpportunities.value.push(newItem);
      break;
    case 'Threats':
      itemsThreats.value.push(newItem);
      break;
  }
};

</script>

<template>
  <header>
    <div class="wrapper">
      <div class="row mt-4 mb-4">
        <div class="col-12 d-flex justify-content-center">
          <h1 class="display-3">Personal SWOT Analysis</h1>
        </div>
      </div>
    </div>
  </header>

  <main>
    <div class="row mt-4 mb-4">
      <SingleCard cardType="bg-primary" header="Strengths" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsStrengths" :key="item.id">{{ item.label }}</li>
        </ul>
      </SingleCard>
      <SingleCard cardType="bg-warning" header="Weaknesses" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsWeaknesses" :key="item.id">{{ item.label }}</li>
        </ul>
      </SingleCard>
    </div>
    <div class="row mt-4 mb-4">
      <SingleCard cardType="bg-success" header="Opportunities" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsOpportunities" :key="item.id">{{ item.label }}</li>
        </ul>
      </SingleCard>
      <SingleCard cardType="bg-danger" header="Threats" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsThreats" :key="item.id">{{ item.label }}</li>
        </ul>
      </SingleCard>
    </div>
    <div class="row mt-4 mb-4">
      <SwotInput :swot-objective="swotAnalysisObjective"  v-on:addItemToSwotChart="addItemToSwotList"></SwotInput>
    </div>
  </main>
</template>

<style scoped>
ul{
  list-style: none;
}
</style>
