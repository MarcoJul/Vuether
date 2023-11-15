<script setup lang="ts">


interface DaysInfo {
  conditions: string;
  temp: number;
  datetime: 'string';
  humidity: number;
  icon: string;
  precipprob: number;
}

const props = defineProps<{
  day: DaysInfo
}>()

</script>


<template>
  <div class="card">
    {{ props.day.datetime }}
        {{ props.day.temp }}<br>
        {{ props.day.conditions }}
  </div>
</template>

<style scoped>
.card {
  font-family: 'Krona One', sans-serif;
  height: 500px;
  width: 150px;
  background-color: #E6DF95;
  border-radius: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>