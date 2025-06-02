<template>
    <main class="container">
      <div class="links">
      </div>
      <h1>Our cars</h1>
      <select @change="handleChange" v-model="make" name="make" id="make">
        <option value="All">All</option>
        <option value="Audi">Audi</option>
        <option value="Chevrolet">Chevrolet</option>
        <option value="Porsche">Porsche</option>
      </select>
      <div class="cards">
        <div 
          v-for="car in cars" 
          :key="car.id" 
          class="card" 
          @click="router.push(`/car/${car.id}`)"
          >
          <h1>{{ car.make }}</h1>
          <p>${{ car.price }}</p>
        </div>
      </div>
    </main>
    
    </template>
    
    <script setup lang="ts">
    import { onMounted, ref, watch } from 'vue';
    import carsData from '../data.json'
    import { useRoute, useRouter } from 'vue-router';
    
    interface ICars {
    id: number;
    make: string;
    body: string;
    price: number;
    year: number;
    }
    
    const router = useRouter();
    const route = useRoute();
    const cars = ref<ICars[]>(carsData);
    const make = ref<string>('All');
    
   watch(make, () => {
    if(make.value) {
      if(make.value === 'All') {
        cars.value = carsData
      }else {
        cars.value = carsData.filter(car => 
          car.make === make.value
        )
      }
    }
   })
    
   const handleChange = () => {
    router.push({
      query: {
        make: make.value
      }
    })
   }

   onMounted(() => {
  console.log('route query', route.query);
  if(typeof route.query.make === 'string') {
    make.value = route.query.make //route.query.make is like query route = /?make=Audi, the make = Audi
  }else {
    make.value = 'All';
  }
  })
    
    
    </script>
    
    <style scoped>
    .cards {
      display: flex;
      width: 1000px;
      flex-wrap: wrap;
      margin-top: 50px;
      justify-content: center;
    }
    
    .card {
      box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.207);
      padding: 15px;
      width: 150px;
      margin-right: 15px;
      cursor: pointer;
      margin-bottom: 20px;
    
    }
    
    </style>