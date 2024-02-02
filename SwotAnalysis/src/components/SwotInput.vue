<script setup>
import { ref } from 'vue'
import SwotEditButton from './SwotEditButton.vue'

defineProps({
  swotObjective: {
    type: String,
  }
})

const addedSwotElement = ref('');

// function updateLocation() {
//   addedSwotElement = 'South Pole'
// }
const clearInput = () => {
  addedSwotElement.value = '';
};

// Expose the method to the parent component
defineExpose({
  clearInput
});

</script>

<template>
  <div class="col-12 d-flex justify-content-center align-items-center">
    <div class="input-group">
      <span class="input-group-text">{{ swotObjective ? swotObjective : 'ggg' }}</span>
      <textarea type="text" class="form-control" v-model="addedSwotElement" placeholder="Add an item"></textarea>
      <SwotEditButton 
        :edit-btn="'Add '+ swotObjective.toLowerCase()" 
        btnType="btn-secondary" 
        @click="$emit('addItemToSwotChart', swotObjective, addedSwotElement)"
        :bind:disabled="addedSwotElement.length === 0"
      >
      </SwotEditButton>
    </div>
  </div>  
</template>