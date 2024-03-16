<template>
    <div class="display-screen-container mb-2">
        <span class="display-screen">{{ props.display }}</span>
    </div>
</template>

<script setup lang="ts">

const props = defineProps({
  display: { type: String, required: true }
})

</script>


<style scoped>
.display-screen-container {
    display: flex;
    justify-content: end;
    align-items: center;
    height: 30px;
    background-color: beige;
    border-radius: 25px;
}

.display-screen {
    padding-right: 20px;
}
</style>