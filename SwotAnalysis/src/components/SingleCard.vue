<script setup>
import { ref } from 'vue'
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
  // swotItem: {
  //   type: Object
  // }
})

</script>

<template>
  <div class="col-sm-6 col-12 d-flex justify-content-center align-items-center">
    <!-- types: bg-primary, bg-success, bg-danger, bg-warning -->
    <div class="card text-white mb-3" :class="cardType" style="width: 18rem;">
      <div class="card-header d-flex justify-content-between">
        {{ header }} 
        <SwotEditButton @click="$emit('displayBtnId', header)" :id="header" edit-btn="Add item" btnType="btn-outline-light ms-5"></SwotEditButton>
      </div>
      <div class="card-body">
        <p class="card-text">
          <slot></slot>
        </p>
      </div>
      <div class="card-footer d-flex justify-content-end">
        <SwotEditButton edit-btn="Remove item" btnType="btn-outline-light ms-5"></SwotEditButton>
      </div>
    </div>
  </div>  
</template>