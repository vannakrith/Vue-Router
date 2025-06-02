<template>

<div class="container">

    <div class="car" v-if="car">
        <h1>Cars</h1>
        <p>Make: {{ car.make }}</p>
        <p>Body: {{ car.body }}</p>
        <p>Price: {{ car.price }}</p>
        <p>Year: {{ car.year }}</p>
    </div>
    <div class="not-found" v-else>
        <h1>Not that car found</h1>
    </div>
</div>

</template>

<script setup lang="ts">
import { useRoute } from 'vue-router';
import { onBeforeMount, ref } from 'vue';
import cars from '../data.json';

const rout = useRoute();
const {id} = rout.params; //Destructuring form, Full form is: `const id = rout.params.id`
const car = ref();

onBeforeMount(() => {
 car.value = cars.find( c => c.id === Number(id))
 console.log('rout params id', rout.params.id);
});

</script>