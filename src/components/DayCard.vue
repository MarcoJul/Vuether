<script setup lang="ts">

import {computed} from 'vue';

import cloudy from '../assets/images/cloudy.svg';

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

const formattedWeekDay = computed(()=> {
  return new Date(props.day.datetime).toLocaleDateString('en-EN', {weekday: 'short'});
});
const formattedDayNumber = computed(()=> {
  return new Date(props.day.datetime).toLocaleDateString('en-EN', {day: 'numeric'});
});


</script>


<template>
  <div class="date-section">
    <p class="weekday">{{ formattedWeekDay }}</p>
    <p class="daynumber">{{ formattedDayNumber }}</p>
  </div>
    <div class="card">
    <img class="weather-image" :src="cloudy"/>
        {{ props.day.temp }}<br>
        {{ props.day.conditions }}
  </div>
</template>

<style scoped>

.date-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: 'Krona One', sans-serif;
}

.weekday {
  text-transform: uppercase;
  font-size: 15px;
}

.daynumber{
  font-size: 50px;
}
.card {
  font-family: 'Krona One', sans-serif;
  height: 500px;
  width: 150px;
  background-color: #E6DF95;
  border-radius: 45px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 14.49122px 5.26953px 44.79104px 0px rgba(32, 77, 92, 0.60), 0px 5.26953px 5.26953px 0px rgba(0, 0, 0, 0.25);
}

.weather-image {
  width: 100px;
  transition: all .3s;
}


.weather-image:hover {
  width: 110px;
}
</style>