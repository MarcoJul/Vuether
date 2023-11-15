<script setup lang="ts">

import { ref, computed } from 'vue';
import type { Ref, ComputedRef } from 'vue';

interface DaysInfo {
  conditions: string;
  temp: number;
  datetime: 'string';
  humidity: number;
  icon: string;
  precipprob: number;
}

const key: string = import.meta.env.VITE_API_KEY;
const days: Ref<any> = ref()
const isLoading = ref(true);

async function getWeather(city: string, key: string) {
  try{
    isLoading.value = true;
    const response = await fetch(`https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${city}?unitGroup=metric&key=${key}&contentType=json`);
    const data = await response.json();
    console.log('data',data);
    days.value = data;
  } catch(e) {
    console.error('There was an error', e);
  } finally {
    isLoading.value = false;
  }
}
getWeather('genoa', key);

const daysShown: ComputedRef<DaysInfo[]> = computed(()=> {
  return days.value.days.slice(0,7);
})

</script>

<template>
  <div class="plain-background">
    <div class="container">
      <p v-if="!isLoading" v-for="day in daysShown">
        {{ day.datetime }}
        {{ day.temp }}<br>
        {{ day.conditions }}
      </p>
      <p v-else>Loading..</p>
    </div>
  </div>
</template>

<style scoped>
  .plain-background {
    background-color: #E9F5FA;
    height: 100vh;
    width: 100%;
    display: flex;
    align-items: center;
  }
  
  .container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-grow: 2;
    gap: 20px;
    margin: 0 35px;
  }
</style>
