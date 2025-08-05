<script setup>
import DataChart from './components/DataChart.vue';
</script>

<template>
  <header>
    <h1></h1>
  </header>
  <main>
    <DataChart />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  text-align: center;
}
main {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 2rem;
}
</style>