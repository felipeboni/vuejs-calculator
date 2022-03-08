<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
import 'bootstrap/dist/css/bootstrap.min.css'
import Calculator from "./components/Calculator.vue";
</script>

<template>
  <Calculator />
</template>

<style>
    body {
        background: #151515;
    }
    .c-font {
        font-family: "San Francisco";
    }
</style>