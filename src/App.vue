<script setup lang="ts">
import CalculatorBase from './components/CalculatorBase.vue'
</script>

<template>
  <div class="fixed-header">
    <label>Vue Calculator Example</label>
    <CalculatorBase></CalculatorBase>
  </div>
  
</template>

<style scoped>
.fixed-header {
    text-align: center;
    position:fixed;
    top:0;
    width: 100%;
}
</style>
