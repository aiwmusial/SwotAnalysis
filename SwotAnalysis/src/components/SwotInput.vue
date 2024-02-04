<script setup>
import { ref } from 'vue'
import SwotEditButton from './SwotEditButton.vue'

defineProps({
  swotObjective: {
    type: String,
  }
})

const addedSwotElement = ref('');

const clearInput = () => {
  addedSwotElement.value = '';
};

defineExpose({
  clearInput
});

</script>

<template>
  <div class="col-12 d-flex justify-content-center align-items-center">
    <div class="input-group  ms-3 me-3">
      <span class="input-group-text">{{ swotObjective }}</span>
      <textarea type="text" class="form-control" v-model="addedSwotElement" placeholder="Add an item"></textarea>
      <SwotEditButton 
        :edit-btn="'Add '+ swotObjective.toLowerCase()" 
        btnType="btn-secondary" 
        @click="$emit('addItemToSwotChart', swotObjective, addedSwotElement)"
        v-bind:disabled="addedSwotElement.length < 3"
      >
      </SwotEditButton>
    </div>
  </div>  
</template>