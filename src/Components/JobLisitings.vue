<script setup>
import { defineProps,ref,onMounted} from 'vue';
import axios from 'axios';
import JobListing from "./JobListing.vue";
import { RouterLink } from 'vue-router';

defineProps({
    limit:Number,
    showButton:{
        type:Boolean,
        default:false
    }
});
const jobs = ref([]);
onMounted(async()=>{
    try{
        const response=await axios.get('/api/jobs');
        console.log("this is my response data ",response.data);
        jobs.value=response.data;
    }catch(error){
        console.log(error);
    }
})
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">Browse Jobs</h2>
      <div class="grid grid-cols-1  md:grid-cols-3 gap-6">
     <JobListing v-for="job in jobs.slice(0, limit)||jobs.length" :key="job.id" :job="job"/>
      </div>
      <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
      <RouterLink
        to="/jobs"
        class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        >View All Jobs</RouterLink>
      
    </section>
    </div>
    
  </section>
 
</template>
