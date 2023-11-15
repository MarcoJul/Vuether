<script setup lang="ts">

import { ref } from 'vue';
import type { Ref } from 'vue'

interface DaysInfo {
  conditions: string;
  temp: number;
  datetime: 'string';
  humidity: number;
  icon: string;
  precipprob: number;
}

const key: string = import.meta.env.VITE_API_KEY;
const days: Ref<DaysInfo[]> = ref([])
const isLoading = ref(true);

async function getWeather(city: string, key: string) {
  try{
    isLoading.value = true;
    const response = await fetch(`https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${city}?unitGroup=metric&key=${key}&contentType=json`);
    const data = await response.json();
    days.value = data.days;
    console.log(days.value);
  } catch(e) {
    console.error('There was an error', e);
  } finally {
    isLoading.value = false;
  }
}

getWeather('genoa', key);

</script>

<template>
  <div>
    <p v-if="!isLoading" v-for="day in days">
      {{ day.temp }}
      {{ day.conditions }}
    </p>
  </div>
</template>

<style scoped>

</style>
