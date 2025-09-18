<script setup>
// Search
import { ref, computed } from 'vue'
import Job from '@/components/job.vue'

let queryRef = ref('')
let query = ''

function performSearch() {
  queryRef.value = query
}

// Categories
let { data: jobCategories } = await useFetch('http://127.0.0.1:8000/api/v1/jobs/categories')
let selectedCategoriesRef = ref([])
let selectedCategories = []

function toggleCategory(id) {
  const index = selectedCategories.indexOf(id)
  if (index === -1) selectedCategories.push(id)
  else selectedCategories.splice(index, 1)
  selectedCategoriesRef.value = [...selectedCategories]
}

// Jobs
let { data: jobsData } = await useFetch('http://127.0.0.1:8000/api/v1/jobs/', {
  query: { query: queryRef, categories: computed(() => selectedCategoriesRef.value.join(',')) }
})

const jobs = computed(() => jobsData.value || [])
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Header -->
    <div class="bg-white border-b border-gray-200">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
        <h1 class="text-2xl font-bold text-gray-900">Browse Jobs</h1>
        <p class="mt-1 text-sm text-gray-600">Find your next opportunity</p>
      </div>
    </div>

    <!-- Main Content -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="flex flex-col lg:flex-row gap-8">
        <!-- Sidebar -->
        <div class="lg:w-80 flex-shrink-0">
          <div class="bg-white rounded-lg border border-gray-200 p-6 sticky top-8">
            <!-- Search -->
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-2">Search Jobs</label>
              <div class="relative">
                <input
                  v-model="query"
                  type="search"
                  placeholder="Job title, company, keyword..."
                  class="w-full px-4 py-2 pl-10 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
                />
                <svg class="absolute left-3 top-2.5 w-4 h-4 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
              </div>
              <button
                @click="performSearch"
                class="w-full mt-3 px-4 py-2 bg-blue-600 text-white text-sm font-medium rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-colors duration-200"
              >
                Search Jobs
              </button>
            </div>

            <!-- Categories -->
            <div>
              <h3 class="text-sm font-medium text-gray-700 mb-3">Categories</h3>
              <div class="space-y-2 max-h-60 overflow-y-auto">
                <label
                  v-for="category in jobCategories"
                  :key="category.id"
                  class="flex items-center cursor-pointer group"
                >
                  <input
                    type="checkbox"
                    :checked="selectedCategoriesRef.includes(category.id)"
                    @change="toggleCategory(category.id)"
                    class="w-4 h-4 text-blue-600 border-gray-300 rounded focus:ring-blue-500 focus:ring-2"
                  />
                  <span class="ml-3 text-sm text-gray-700 group-hover:text-gray-900">
                    {{ category.title }}
                  </span>
                </label>
              </div>
            </div>
          </div>
        </div>

        <!-- Job List -->
        <div class="flex-1">
          <!-- Results Header -->
          <div class="bg-white rounded-lg border border-gray-200 p-4 mb-6">
            <div class="flex items-center justify-between">
              <div>
                <h2 class="text-lg font-semibold text-gray-900">
                  {{ jobs.length }} {{ jobs.length === 1 ? 'Job' : 'Jobs' }} Found
                </h2>
                <p class="text-sm text-gray-600 mt-1" v-if="queryRef || selectedCategoriesRef.length > 0">
                  <span v-if="queryRef">Searching for "{{ queryRef }}"</span>
                  <span v-if="queryRef && selectedCategoriesRef.length > 0"> • </span>
                  <span v-if="selectedCategoriesRef.length > 0">
                    {{ selectedCategoriesRef.length }} {{ selectedCategoriesRef.length === 1 ? 'category' : 'categories' }} selected
                  </span>
                </p>
              </div>
              
              <!-- Clear Filters -->
              <button
                v-if="queryRef || selectedCategoriesRef.length > 0"
                @click="queryRef = ''; query = ''; selectedCategoriesRef = []; selectedCategories = []"
                class="text-sm text-blue-600 hover:text-blue-700 font-medium"
              >
                Clear Filters
              </button>
            </div>
          </div>

          <!-- Jobs -->
          <div class="space-y-4">
            <Job
              v-for="job in jobs"
              :key="job.id"
              :job="job"
              :my="false"
            />
            
            <!-- Empty State -->
            <div v-if="jobs.length === 0" class="bg-white rounded-lg border border-gray-200 p-12 text-center">
              <svg class="w-12 h-12 text-gray-400 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
              </svg>
              <h3 class="text-lg font-medium text-gray-900 mb-2">No jobs found</h3>
              <p class="text-gray-600 mb-4">Try adjusting your search criteria or browse all available positions.</p>
              <button
                @click="queryRef = ''; query = ''; selectedCategoriesRef = []; selectedCategories = []"
                class="inline-flex items-center px-4 py-2 bg-blue-600 text-white text-sm font-medium rounded-md hover:bg-blue-700 transition-colors duration-200"
              >
                View All Jobs
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>