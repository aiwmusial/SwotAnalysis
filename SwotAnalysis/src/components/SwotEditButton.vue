<script setup>
defineProps({
    editBtn: {
        type: String
    },
    btnType: {
        type: String
    }
})
</script>


<template>
    <button type="button" class="btn btn-sm" :class="btnType">{{ editBtn }}</button>
</template>  