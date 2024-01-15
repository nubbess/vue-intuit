<template>
    <div class="carta">
        <div class="card" style="width: 18rem;">
            <div class="card-body">
                <img :src="icon">
                <h5 class="card-title">{{ ciudad }}</h5>
                <p class="card-text"> {{ pais }}</p>
                <a href="#" class="card-link"> {{ temperature }}</a>
                <a href="#" class="card-link"> {{ weather }}</a>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        icon: String,
        ciudad: String,
        pais: String,
        temperature: String,
        weather: String,
        pressure: String,
    })
</script>

<style scoped>
    img {
        width:30px;
        margin-bottom: 10px
    }
</style>