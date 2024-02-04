<script setup>
import SwotEditButton from './SwotEditButton.vue'

defineProps({
  header: {
    type: String,
    required: true
  },
  cardType: {
    type: String
  },
  swotList:{
    type: String
  }
})

</script>

<template>
  <div class="col-sm-6 col-12 d-flex justify-content-center align-items-center">
    <!-- types: bg-primary, bg-success, bg-danger, bg-warning -->
    <div class="card text-white w-100 mb-3 ms-3 me-3 overflow-auto" :class="cardType" style="height: 20rem;">
      <div class="card-header d-flex justify-content-between">
        {{ header }} 
        <SwotEditButton 
          @click="$emit('displayBtnId', header)" 
          :id="header" 
          edit-btn="Add item" 
          btnType="btn-outline-light ms-3"
        >
        </SwotEditButton>
      </div>
      <div class="card-body">
        <p class="card-text">
          <slot></slot>
        </p>
      </div>
      <div class="card-footer d-flex justify-content-end">
        <SwotEditButton 
          edit-btn="Remove item" 
          btnType="btn-outline-light ms-5"
          @click="$emit('removeItemFromSwotChart', header)"
        >
        </SwotEditButton>
      </div>
    </div>
  </div>  
</template>