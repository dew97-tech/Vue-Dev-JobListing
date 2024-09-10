<script setup>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
import { RouterView } from "vue-router";
</script>

<template>
   <div class="min-h-screen flex flex-col">
      <!-- Navbar at the top -->
      <Navbar />

      <!-- Main content should grow to take up space between navbar and footer -->
      <main class="flex-grow">
         <RouterView />
      </main>

      <!-- Footer at the bottom -->
      <Footer />
   </div>
</template>
