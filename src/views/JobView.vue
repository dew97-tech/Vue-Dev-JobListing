<script setup>
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import { reactive, onMounted } from "vue";
import { useRoute, RouterLink, useRouter } from "vue-router";
import BackButton from "@/components/BackButton.vue";
import { useToast } from "vue-toastification";
const route = useRoute();
const router = useRouter();
const toast = useToast();

const jobId = route.params.id;

const state = reactive({
   job: {},
   isLoading: true,
});
const deleteJob = async () => {
   try {
      const response = await fetch(`/api/jobs/${jobId}`, {
         method: "DELETE",
      });
      if (response.ok) {
         toast.success("Job deleted successfully");
         router.push("/jobs");
      } else {
         toast.error("Error deleting job");
      }
   } catch (error) {
      console.error("Error deleting job", error);
      toast.error("Error deleting job");
   }
};
onMounted(async () => {
   try {
      const response = await fetch(`/api/jobs/${jobId}`);
      const data = await response.json();
      state.job = data;
   } catch (error) {
      console.error("Error fetching job", error);
   } finally {
      state.isLoading = false;
   }
});
</script>

<template>
   <BackButton />
   <section v-if="!state.isLoading" class="bg-green-50">
      <div class="container m-auto py-10 px-6">
         <div class="grid grid-cols-1 md:grid-cols-70/30 w-full gap-6">
            <main>
               <div class="bg-white p-6 rounded-lg shadow-md">
                  <h2 class="text-3xl font-bold text-green-500 mb-6">{{ state.job.title }}</h2>

                  <div class="text-gray-600 my-2">{{ state.job.type }}</div>

                  <div class="mb-6">
                     <h3 class="text-xl font-bold">Description</h3>
                     <p class="my-2">{{ state.job.description }}</p>
                  </div>

                  <div class="mb-6">
                     <h3 class="text-xl font-bold">Salary</h3>
                     <p class="my-2 text-green-500 font-bold">{{ state.job.salary }} / Year</p>
                  </div>

                  <div class="mb-6">
                     <h3 class="text-xl font-bold">Location</h3>
                     <p class="my-2 text-orange-700 font-bold">
                        <i class="pi pi-map-marker text-orange-700"></i>
                        {{ state.job.location }}
                     </p>
                  </div>

                  <div class="mb-6">
                     <h3 class="text-xl font-bold">Company</h3>
                     <p class="my-2">{{ state.job.company?.name }}</p>
                  </div>

                  <div class="mb-6">
                     <h3 class="text-xl font-bold">Contact Email</h3>
                     <p class="my-2 bg-green-100 p-2 font-bold">{{ state.job.company?.contactEmail }}</p>
                  </div>

                  <div class="mb-6">
                     <h3 class="text-xl font-bold">Contact Phone</h3>
                     <p class="my-2 bg-green-100 p-2 font-bold">{{ state.job.company?.contactPhone }}</p>
                  </div>
               </div>
            </main>

            <!-- Sidebar -->
            <aside>
               <!-- Company Info -->
               <div class="bg-white p-6 rounded-lg shadow-md">
                  <h3 class="text-xl font-bold mb-6">Company Info</h3>

                  <h2 class="text-2xl">{{ state.job.company?.name }}</h2>

                  <p class="my-2">
                     {{ state.job.company?.description }}
                  </p>

                  <hr class="my-4" />

                  <h3 class="text-xl">Contact Email:</h3>

                  <p class="my-2 bg-green-100 p-2 font-bold">{{ state.job.company?.contactEmail }}</p>

                  <h3 class="text-xl">Contact Phone:</h3>

                  <p class="my-2 bg-green-100 p-2 font-bold">{{ state.job.company?.contactPhone }}</p>
               </div>

               <!-- Manage -->
               <div class="bg-white p-6 rounded-lg shadow-md mt-6">
                  <h3 class="text-xl font-bold mb-6">Manage Job</h3>
                  <RouterLink
                     :to="`/jobs/edit/${state.job.id}`"
                     class="bg-green-500 hover:bg-green-600 text-white text-center font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
                     >Edit Job</RouterLink
                  >
                  <button
                     @click="deleteJob"
                     class="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
                  >
                     Delete Job
                  </button>
               </div>
            </aside>
         </div>
      </div>
   </section>
   <div v-else class="text-center text-gray-500 py-6">
      <PulseLoader color="#38a169" size="10px" />
   </div>
</template>
