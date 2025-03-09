<script setup>
import axios from 'axios';
import JobListing from '@/components/JobListing.vue';
import { reactive, defineProps, onMounted } from 'vue'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
defineProps({
    limit: Number
})
const state = reactive({
    jobs:[],
    isLoading :true
});

onMounted(async()=>{
    try {
        const response = await axios.get('/api/jobs')
        state.jobs = response.data;
    } catch (error) {
        
    }finally{
        state.isLoading = false;
    }
})
</script>
<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div v-if="state.isLoading" class="text-center text-gray">
                <PulseLoader />
            </div>
            <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>

    <section v-if="state.jobs.length > 3" class="m-auto max-w-lg my-10 px-6">
      <a
        :href="'/jobs'"
        class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        >View All Jobs</a
      >
    </section>
</template>