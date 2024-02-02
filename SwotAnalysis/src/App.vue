<script setup>
import { ref } from 'vue';
import SingleCard from './components/SingleCard.vue';
import SwotInput from './components/SwotInput.vue';

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

const swotAnalysisObjective = ref('');
function displayBtnIdOnInput(header){
  swotAnalysisObjective.value = header;
};

const itemsStrengths = ref(JSON.parse(localStorage.getItem("itemsStrengths") || '[]'));
const itemsWeaknesses = ref(JSON.parse(localStorage.getItem("itemsWeaknesses") || '[]'));
const itemsOpportunities = ref(JSON.parse(localStorage.getItem("itemsOpportunities") || '[]'));
const itemsThreats = ref(JSON.parse(localStorage.getItem("itemsThreats") || '[]'));

const swotInputRef = ref(null);

const addItemToSwotList = (swotObjective, addedSwotElement) => {
  console.log(addedSwotElement)
  const newItem = { id: Date.now(), label: addedSwotElement };
  switch(swotObjective) {
    case 'Strengths':
      itemsStrengths.value.push(newItem);
      window.localStorage.setItem("itemsStrengths", JSON.stringify(itemsStrengths.value));
      swotInputRef.value.clearInput();
      break;
    case 'Weaknesses':
      itemsWeaknesses.value.push(newItem);
      window.localStorage.setItem("itemsWeaknesses", JSON.stringify(itemsWeaknesses.value));
      swotInputRef.value.clearInput();
      break;
    case 'Opportunities':
      itemsOpportunities.value.push(newItem);
      window.localStorage.setItem("itemsOpportunities", JSON.stringify(itemsOpportunities.value));
      swotInputRef.value.clearInput();
      break;
    case 'Threats':
      itemsThreats.value.push(newItem);
      window.localStorage.setItem("itemsThreats", JSON.stringify(itemsThreats.value));
      swotInputRef.value.clearInput();
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
        <p v-if="!itemsStrengths.length">Please add you strength</p>
      </SingleCard>
      <SingleCard cardType="bg-warning" header="Weaknesses" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsWeaknesses" :key="item.id">{{ item.label }}</li>
        </ul>
        <p v-if="!itemsWeaknesses.length">Please add you weakness</p>
      </SingleCard>
    </div>
    <div class="row mt-4 mb-4">
      <SingleCard cardType="bg-success" header="Opportunities" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsOpportunities" :key="item.id">{{ item.label }}</li>
        </ul>
        <p v-if="!itemsOpportunities.length">Please add an opportunity</p>
      </SingleCard>
      <SingleCard cardType="bg-danger" header="Threats" v-on:displayBtnId="displayBtnIdOnInput">
        <ul>
          <li v-for="item in itemsThreats" :key="item.id">{{ item.label }}</li>
        </ul>
        <p v-if="!itemsThreats.length">Please add a threat</p>
      </SingleCard>
    </div>
    <div class="row mt-4 mb-4">
      <SwotInput ref="swotInputRef" :swot-objective="swotAnalysisObjective"  v-on:addItemToSwotChart="addItemToSwotList"></SwotInput>
    </div>
  </main>
</template>

<style scoped>
ul{
  list-style: none;
}
</style>
