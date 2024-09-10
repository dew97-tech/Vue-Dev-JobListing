<script setup>
const currentYear = new Date().getFullYear();
import { RouterLink } from "vue-router";
</script>

<template>
   <footer class="bg-green-700 text-white py-8">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
         <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <!-- About Section -->
            <div>
               <h3 class="text-lg font-semibold mb-4">About Vue Jobs</h3>
               <p class="text-sm">
                  Vue Jobs is a platform dedicated to helping developers find their dream Vue.js jobs and for employers
                  to find the right talent.
               </p>
            </div>

            <!-- Quick Links -->
            <div class="flex flex-col">
               <h3 class="text-lg font-semibold mb-4">Quick Links</h3>
               <ul class="flex justify-start gap-4">
                  <li class="mb-2">
                     <RouterLink to="/" class="hover:underline">Home</RouterLink>
                  </li>
                  <li class="mb-2">
                     <RouterLink to="/jobs" class="hover:underline">Jobs</RouterLink>
                  </li>
                  <li class="mb-2">
                     <RouterLink to="/jobs/add" class="hover:underline">Add Job</RouterLink>
                  </li>
                  <li class="mb-2">
                     <RouterLink to="/contact" class="hover:underline">Contact Us</RouterLink>
                  </li>
               </ul>
            </div>

            <!-- Contact Section -->
            <div>
               <h3 class="text-lg font-semibold mb-4">Contact Us</h3>
               <p class="text-sm">
                  Email: <a href="mailto:info@vuejobs.com" class="hover:underline">info@vuejobs.com</a>
               </p>
               <p class="text-sm">Phone: +1 (123) 456-7890</p>

               <div class="mt-4 flex space-x-4">
                  <a href="#" class="hover:text-gray-300">
                     <i class="fab fa-facebook text-2xl"></i>
                  </a>
                  <a href="#" class="hover:text-gray-300">
                     <i class="fab fa-twitter text-2xl"></i>
                  </a>
                  <a href="#" class="hover:text-gray-300">
                     <i class="fab fa-linkedin text-2xl"></i>
                  </a>
               </div>
            </div>
         </div>

         <div class="mt-8 text-center border-t border-green-500 pt-4">
            <p class="text-lg">&copy; {{ currentYear }} Vue Jobs. All rights reserved.</p>
         </div>
      </div>
   </footer>
</template>
