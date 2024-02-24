<script setup>
import { ref, onMounted } from 'vue';

const items = ref([]);

const fetchData = async () => {
    try {
        const response = await fetch(' https://animechan.xyz/api/random');
        const data = await response.json();

        items.value = data;
    } catch (error) {
        console.error('Error fetching data:', error);
    }
};

onMounted(() => fetchData());

</script>

<template>
    <div class="bg-white py-2 px-3 rounded-lg shadow-xl border-2 border-lime-500 w-56 hover:bg-lime-500 hover:text-white">
        <div v-for="(value, key) in items" :key="key" class="font-semibold mb-2">
            <span class="font-bold">{{ key }}</span>: <span>{{ value }}</span>
        </div>
    </div>
</template>

  
<style scoped></style>
  