<template>

<div class="container">

    <div class="car" v-if="car">
        <h1>Cars</h1>
        <p>Make: {{ car.make }}</p>
        <p>Body: {{ car.body }}</p>
        <p>Price: ${{ car.price }}</p>
        <p>Year: {{ car.year }}</p>
        <div class="router-link">
            <RouterLink :to="`/car/${car.id}/dealer`">View Dealer</RouterLink>
            <RouterLink :to="`/car/${car.id}/manufactor`">View Manufactor</RouterLink>
        </div>
        <router-view/>
    </div>
    <div class="not-found" v-else>
        <h1>Not that car found</h1>
    </div>
    <button @click="router.back()">Go back</button>
</div>

</template>

<script setup lang="ts">
import { useRoute, RouterView, RouterLink, useRouter } from 'vue-router';
import { onBeforeMount, ref } from 'vue';
import cars from '../data.json';

const rout = useRoute();
const {id} = rout.params; //Destructuring form, Full form is: `const id = rout.params.id`
const car = ref();
const router = useRouter();

onBeforeMount(() => {
 car.value = cars.find( c => c.id === Number(id))
 console.log('rout params id', rout.params.id);
});

</script>

<style scoped>

.container {
    width: 750px;
}
.car {
    display: flex;
    flex-direction: column;
}
.router  {
    display: flex;
    justify-content: space-between;
}

.router-link>a:last-child {
    margin-left: 32px;
}

</style>