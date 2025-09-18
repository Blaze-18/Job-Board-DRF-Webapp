<script setup>
const route = useRoute()

const {data: job} = await useFetch('http://127.0.0.1:8000/api/v1/jobs/' + route.params.id + '/')
</script>

<template>
    <div class="min-h-screen bg-gray-50">
        <!-- Header -->
        <div class="bg-white border-b">
        <div class="max-w-4xl mx-auto px-4 py-6">
            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
            <div>
                <h1 class="text-2xl font-semibold text-gray-900 mb-1">
                {{ job.title || 'Job Title' }}
                </h1>
                <div class="flex items-center gap-2 text-gray-600">
                <span>{{ job.company_name || 'Company Name' }}</span>
                <span class="text-gray-400">•</span>
                <span>{{ job.position_location || 'Location' }}</span>
                </div>
            </div>
            
            <a 
                :href="'mailto:' + job.company_email" 
                class="inline-flex items-center gap-2 px-4 py-2 bg-teal-600 text-white text-sm font-medium rounded-lg hover:bg-teal-700 transition-colors duration-200"
            >
                Apply Now
            </a>
            </div>
        </div>
        </div>

        <!-- Content -->
        <div class="max-w-4xl mx-auto px-4 py-8">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Description -->
            <div class="lg:col-span-2">
            <div class="bg-white rounded-lg p-6 shadow-sm">
                <h2 class="font-medium text-gray-900 mb-4">Description</h2>
                <div class="text-gray-700 text-sm leading-relaxed whitespace-pre-line">
                {{ job.description || 'Job description not available.' }}
                </div>
            </div>
            </div>

            <!-- Details -->
            <div class="space-y-4">
            <!-- Company -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
                <h3 class="font-medium text-gray-900 mb-3 text-sm">Company</h3>
                <div class="space-y-2 text-sm">
                <div>
                    <span class="text-gray-500">Name</span>
                    <p class="text-gray-900">{{ job.company_name || 'Not specified' }}</p>
                </div>
                <div>
                    <span class="text-gray-500">Location</span>
                    <p class="text-gray-900">{{ job.company_location || 'Not specified' }}</p>
                </div>
                </div>
            </div>

            <!-- Position -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
                <h3 class="font-medium text-gray-900 mb-3 text-sm">Position</h3>
                <div class="space-y-2 text-sm">
                <div>
                    <span class="text-gray-500">Location</span>
                    <p class="text-gray-900">{{ job.position_location || 'Not specified' }}</p>
                </div>
                <div>
                    <span class="text-gray-500">Salary</span>
                    <p class="text-gray-900">{{ job.position_salary || 'Not specified' }}</p>
                </div>
                </div>
            </div>

            <!-- Meta -->
            <div class="bg-white rounded-lg p-4 shadow-sm">
                <div class="text-sm">
                <span class="text-gray-500">Posted</span>
                <p class="text-gray-900">{{ job.created_at_formatted || 'Not available' }}</p>
                </div>
            </div>

            <!-- Mobile Apply -->
            <div class="lg:hidden">
                <a 
                :href="'mailto:' + job.company_email" 
                class="w-full inline-flex items-center justify-center gap-2 px-4 py-2 bg-gray-900 text-white text-sm font-medium rounded-lg hover:bg-gray-800 transition-colors duration-200"
                >
                Apply Now
                </a>
            </div>
            </div>
        </div>
        </div>
    </div>
</template>