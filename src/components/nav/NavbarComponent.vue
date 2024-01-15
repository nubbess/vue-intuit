<template>
    <nav class="navbar bg-body-tertiary">
        <div class="container-fluid">
        <a class="navbar-brand" href="">
            {{ nombreWeb }}
        </a>
        </div>
    </nav>
</template>
<script setup>
    import { defineProps } from 'vue';
    const props = defineProps({
        nombreWeb: String,
    })
</script>
