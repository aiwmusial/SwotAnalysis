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

const inputElementVisible = ref(false)
const swotAnalysisObjective = ref('');
const itemsStrengths = ref(JSON.parse(localStorage.getItem("itemsStrengths") || '[]'));
const itemsWeaknesses = ref(JSON.parse(localStorage.getItem("itemsWeaknesses") || '[]'));
const itemsOpportunities = ref(JSON.parse(localStorage.getItem("itemsOpportunities") || '[]'));
const itemsThreats = ref(JSON.parse(localStorage.getItem("itemsThreats") || '[]'));
const swotInputRef = ref(null);
const swotElementToRemove = ref('');

function displayBtnIdOnInput(header){
  swotAnalysisObjective.value = header;
  inputElementVisible.value = true;
  window.scrollTo({
    top: document.documentElement.scrollHeight,
    behavior: 'smooth',
  });

};

const addItemToSwotList = (swotObjective, addedSwotElement) => {
  const newItem = { id: Date.now(), label: addedSwotElement };
  switch(swotObjective) {
    case 'Strengths':
      itemsStrengths.value.push(newItem);
      window.localStorage.setItem("itemsStrengths", JSON.stringify(itemsStrengths.value));
      break;
    case 'Weaknesses':
      itemsWeaknesses.value.push(newItem);
      window.localStorage.setItem("itemsWeaknesses", JSON.stringify(itemsWeaknesses.value));
      break;
    case 'Opportunities':
      itemsOpportunities.value.push(newItem);
      window.localStorage.setItem("itemsOpportunities", JSON.stringify(itemsOpportunities.value));
      break;
    case 'Threats':
      itemsThreats.value.push(newItem);
      window.localStorage.setItem("itemsThreats", JSON.stringify(itemsThreats.value));
      break;
  }
  swotInputRef.value.clearInput();
  inputElementVisible.value = false;
};

const removeItemFromSwotList = (header) => {
  let index;
  switch(header) {
    case 'Strengths':
      index = itemsStrengths.value.findIndex(item => item.id === swotElementToRemove.value);
      if (index !== -1) {
        itemsStrengths.value.splice(index, 1);
      }
      window.localStorage.setItem("itemsStrengths", JSON.stringify(itemsStrengths.value));
      break;
    case 'Weaknesses':
      index = itemsWeaknesses.value.findIndex(item => item.id === swotElementToRemove.value);
      if (index !== -1) {
        itemsWeaknesses.value.splice(index, 1);
      }
      window.localStorage.setItem("itemsWeaknesses", JSON.stringify(itemsWeaknesses.value));
      break;
    case 'Opportunities':
      index = itemsOpportunities.value.findIndex(item => item.id === swotElementToRemove.value);
      if (index !== -1) {
        itemsOpportunities.value.splice(index, 1);
      }
      window.localStorage.setItem("itemsOpportunities", JSON.stringify(itemsOpportunities.value));
      break;
    case 'Threats':
      index = itemsThreats.value.findIndex(item => item.id === swotElementToRemove.value);
      if (index !== -1) {
        itemsThreats.value.splice(index, 1);
      }    
      window.localStorage.setItem("itemsThreats", JSON.stringify(itemsThreats.value));
      break;
  }
  swotElementToRemove.value = "";
}
</script>

<template>
  <div class="container-fluid">
    <header>
      <div class="wrapper">
        <div class="row mt-4 mb-4">
          <div class="col-12 d-flex justify-content-center">
            <h1 class="text-body-secondary">Personal SWOT Analysis</h1>
          </div>
          <div class="col-8 d-flex justify-content-center mx-auto">
            <p class="lead text-center">
              SWOT analysis is a simple chart used for planning and making better decisions. 
              <br>
              It examines both outside factors (Opportunities and Threats) and inside factors (Strengths and Weaknesses). 
              <br>
              This method is great for finding out what might be stopping you from doing better and also helps identify good opportunities. It's a powerful step in developing strategies to improve and grow.
              <br>
              Do your own SWOT analysis. Everything you put in is kept safe in your browser. Come back in a few days to think it over. Then, make a move! 
              <br>
              <b>Good luck!</b>       
            </p>
          </div>
        </div>
      </div>
    </header>
    <main>
      <div class="row mt-4 mb-4 ms-5 me-5">
        <SingleCard 
          cardType="bg-primary" 
          header="Strengths" 
          v-on:displayBtnId="displayBtnIdOnInput"
          v-on:removeItemFromSwotChart="removeItemFromSwotList"        
        >
          <ul>
            <li 
              v-for="item in itemsStrengths"
            >
              <div class="form-check">
                <input class="form-check-input" type="radio" name="radioSelect" :value="item.id" v-model="swotElementToRemove">
                <label class="form-check-label" :for="item.id">{{ item.label }}</label>
              </div>
            </li>
          </ul>
          <p v-if="!itemsStrengths.length">Please add you strength</p>
        </SingleCard>
        <SingleCard 
          cardType="bg-warning" 
          header="Weaknesses" 
          v-on:displayBtnId="displayBtnIdOnInput"
          v-on:removeItemFromSwotChart="removeItemFromSwotList"        
        >
          <ul>
            <li 
              v-for="item in itemsWeaknesses"
              >
                <div class="form-check">
                  <input class="form-check-input" type="radio" name="radioSelect" :value="item.id" v-model="swotElementToRemove">
                  <label class="form-check-label" :for="item.id">{{ item.label }}</label>
                </div>
              </li>
          </ul>
          <p v-if="!itemsWeaknesses.length">Please add you weakness</p>
        </SingleCard>
      </div>
      <div class="row mt-4 mb-4 ms-5 me-5">
        <SingleCard 
          cardType="bg-success" 
          header="Opportunities" 
          v-on:displayBtnId="displayBtnIdOnInput" 
          v-on:removeItemFromSwotChart="removeItemFromSwotList"
        >
          <ul>
            <li 
              v-for="item in itemsOpportunities"
              >
                <div class="form-check">
                  <input class="form-check-input" type="radio" name="radioSelect" :value="item.id" v-model="swotElementToRemove">
                  <label class="form-check-label" :for="item.id">{{ item.label }}</label>
                </div>  
              </li>
          </ul>
          <p v-if="!itemsOpportunities.length">Please add an opportunity</p>
        </SingleCard>
        <SingleCard 
          cardType="bg-danger" 
          header="Threats" 
          v-on:displayBtnId="displayBtnIdOnInput"
          v-on:removeItemFromSwotChart="removeItemFromSwotList"        
        >
          <ul>
            <li 
              v-for="item in itemsThreats"
              >
                <div class="form-check">
                  <input class="form-check-input" type="radio" name="radioSelect" :value="item.id" v-model="swotElementToRemove">
                  <label class="form-check-label" :for="item.id">{{ item.label }}</label>
                </div>
              </li>
          </ul>
          <p v-if="!itemsThreats.length">Please add a threat</p>
        </SingleCard>
      </div>
      <div class="row mt-4 mb-4 ms-5 me-5">
        <SwotInput 
          v-if="inputElementVisible" 
          ref="swotInputRef" 
          :swot-objective="swotAnalysisObjective"  
          v-on:addItemToSwotChart="addItemToSwotList"
        >
        </SwotInput>
      </div>
    </main>
    <footer class="bg-white">
        <div class="text-center container-fluid text-body-secondary">
          <div class="row">
            <div class="col">
              <h5 class="px-3 text-body-secondary text-light text-uppercase">&copy;2021 Anna Musiał</h5>
            </div>
          </div>
        </div>
      </footer>
  </div>
</template>

<style scoped>
ul{
  list-style: none;
}
.form-check-input:checked{
  background-color: #fd7e14;
  border-color: #fd7e14;
}
</style>
