<script setup>
import router from '@/router';
import { reactive } from 'vue';
import axios from 'axios';
import { useToast } from 'vue-toastification';

const toast = useToast();

const form = reactive({
    type: 'Full-Time',
    title: '',
    description: '',
    salary: '',
    location: '',
    company: {
        name: '',
        description: '',
        contactEmail: '',
        contactPhone: '',
    },
})

const handleSubmit = async () => {
    const newJob = {
        title: form.title,
        type: form.type,
        location: form.location,
        description: form.description,
        salary: form.salary,
        company: {
            name: form.company.name,
            description: form.company.description,
            contactEmail: form.company.contactEmail,
            contactPhone: form.company.contactPhone,
        },
    }


    try {
        const response = await axios.post('/api/jobs', newJob);
        toast.success('Job Added Successfully');

        router.push(`/jobs/${response.data.id}`);
    } catch (error) {
        console.error('Error fetching job', error);
        toast.error('Job Was Not Added');
    }
}
</script>
<template>
    <section class="bg-gradient-to-r from-green-50 to-blue-50 py-16">
        <div class="container m-auto max-w-2xl">
            <div
                class="bg-white px-8 py-10 mb-4 shadow-lg rounded-lg border border-gray-100 transform transition-all hover:scale-105">
                <form @submit.prevent="handleSubmit">
                    <h2 class="text-4xl text-center font-bold mb-8 text-gray-800">Add Job</h2>

                    <!-- Job Type -->
                    <div class="mb-6">
                        <label for="type" class="block text-gray-700 font-bold mb-2">Job Type</label>
                        <select id="type" name="type" v-model="form.type"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            required>
                            <option value="Full-Time">Full-Time</option>
                            <option value="Part-Time">Part-Time</option>
                            <option value="Remote">Remote</option>
                            <option value="Internship">Internship</option>
                        </select>
                    </div>

                    <!-- Job Listing Name -->
                    <div class="mb-6">
                        <label class="block text-gray-700 font-bold mb-2">Job Listing Name</label>
                        <input type="text" id="name" name="name" v-model="form.title"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            placeholder="eg. Beautiful Apartment In Miami" required />
                    </div>

                    <!-- Description -->
                    <div class="mb-6">
                        <label for="description" class="block text-gray-700 font-bold mb-2">Description</label>
                        <textarea id="description" name="description" v-model="form.description"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            rows="4" placeholder="Add any job duties, expectations, requirements, etc"></textarea>
                    </div>

                    <!-- Salary -->
                    <div class="mb-6">
                        <label for="salary" class="block text-gray-700 font-bold mb-2">Salary</label>
                        <select id="salary" name="salary" v-model="form.salary"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            required>
                            <option value="Under $50K">Under $50K</option>
                            <option value="$50K - $60K">$50K - $60K</option>
                            <option value="$60K - $70K">$60K - $70K</option>
                            <option value="$70K - $80K">$70K - $80K</option>
                            <option value="$80K - $90K">$80K - $90K</option>
                            <option value="$90K - $100K">$90K - $100K</option>
                            <option value="$100K - $125K">$100K - $125K</option>
                            <option value="$125K - $150K">$125K - $150K</option>
                            <option value="$150K - $175K">$150K - $175K</option>
                            <option value="$175K - $200K">$175K - $200K</option>
                            <option value="Over $200K">Over $200K</option>
                        </select>
                    </div>

                    <!-- Location -->
                    <div class="mb-6">
                        <label class="block text-gray-700 font-bold mb-2">Location</label>
                        <input type="text" id="location" name="location"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            placeholder="Company Location" required />
                    </div>

                    <!-- Company Info Section -->
                    <h3 class="text-2xl font-bold mb-6 text-gray-800">Company Info</h3>

                    <!-- Company Name -->
                    <div class="mb-6">
                        <label for="company" class="block text-gray-700 font-bold mb-2">Company Name</label>
                        <input type="text" id="company" name="company" v-model="form.company.name"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            placeholder="Company Name" />
                    </div>

                    <!-- Company Description -->
                    <div class="mb-6">
                        <label for="company_description" class="block text-gray-700 font-bold mb-2">Company
                            Description</label>
                        <textarea id="company_description" name="company_description" v-model="form.company.description"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            rows="4" placeholder="What does your company do?"></textarea>
                    </div>

                    <!-- Contact Email -->
                    <div class="mb-6">
                        <label for="contact_email" class="block text-gray-700 font-bold mb-2">Contact Email</label>
                        <input type="email" id="contact_email" name="contact_email" v-model="form.company.contactEmail"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            placeholder="Email address for applicants" required />
                    </div>

                    <!-- Contact Phone -->
                    <div class="mb-6">
                        <label for="contact_phone" class="block text-gray-700 font-bold mb-2">Contact Phone</label>
                        <input type="tel" id="contact_phone" name="contact_phone" v-model="form.company.contactPhone"
                            class="border rounded-lg w-full py-3 px-4 focus:ring-2 focus:ring-green-500 focus:border-green-500 transition-all"
                            placeholder="Optional phone for applicants" />
                    </div>

                    <!-- Submit Button -->
                    <div class="mt-8">
                        <button
                            class="bg-gradient-to-r from-green-500 to-blue-500 hover:from-green-600 hover:to-blue-600 text-white font-bold py-3 px-6 rounded-lg w-full focus:outline-none focus:ring-2 focus:ring-green-500 transition-all transform hover:scale-105"
                            type="submit">
                            Add Job
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </section>
</template>