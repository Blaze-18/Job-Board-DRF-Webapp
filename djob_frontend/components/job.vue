<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()
const emit = defineEmits(['deleteJob'])

const props = defineProps({
  my: { type: Boolean, default: false },
  job: { type: Object, required: true }
})

async function deleteJob(id) {
  try {
    await $fetch(`http://127.0.0.1:8000/api/v1/jobs/${id}/delete/`, {
      method: 'DELETE',
      headers: {
        Authorization: 'token ' + userStore.user.token,
        'Content-Type': 'application/json'
      }
    })
    emit('deleteJob', id)
  } catch (error) {
    console.error(error)
  }
}
</script>

<template>
  <div class="bg-white border border-gray-200 rounded-lg p-6 hover:shadow-sm transition-shadow duration-200">
    <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4">
      <!-- Job Information -->
      <div class="flex-1 min-w-0">
        <div class="flex flex-col md:flex-row md:items-start gap-4">
          <!-- Title and Company -->
          <div class="flex-1 min-w-0">
            <h3 class="text-lg font-semibold text-gray-900 truncate mb-1">
              {{ job.title || 'Untitled Job' }}
            </h3>
            <p class="text-sm text-gray-600 mb-3">
              {{ job.company_name || 'Unknown Company' }}
            </p>
            
            <!-- Location and Salary -->
            <div class="flex flex-col sm:flex-row sm:items-center gap-2 text-sm text-gray-700">
              <div class="flex items-center gap-1">
                <svg class="w-4 h-4 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
                <span>{{ job.position_location || 'Location not specified' }}</span>
              </div>
              
              <div class="hidden sm:block text-gray-300">•</div>
              
              <div class="flex items-center gap-1">
                <svg class="w-4 h-4 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1" />
                </svg>
                <span>{{ job.position_salary || 'Salary not specified' }}</span>
              </div>
            </div>
          </div>
          
          <!-- Posted Date -->
          <div class="text-xs text-gray-500 md:text-right whitespace-nowrap">
            <span>Posted {{ job.created_at_formatted || '-' }}</span>
          </div>
        </div>
      </div>
      
      <!-- Actions -->
      <div class="flex items-center gap-2 pt-4 md:pt-0 border-t md:border-t-0 md:border-l md:pl-4">
        <NuxtLink 
          :to="'/browse/' + job.id" 
          class="inline-flex items-center px-3 py-2 text-sm font-medium text-blue-700 bg-blue-50 border border-blue-200 rounded-md hover:bg-blue-100 hover:border-blue-300 transition-colors duration-200"
        >
          View Details
        </NuxtLink>
        
        <NuxtLink 
          v-if="my" 
          :to="'/editjob/' + job.id" 
          class="inline-flex items-center px-3 py-2 text-sm font-medium text-gray-700 bg-gray-50 border border-gray-200 rounded-md hover:bg-gray-100 hover:border-gray-300 transition-colors duration-200"
        >
          Edit
        </NuxtLink>
        
        <button 
          v-if="my" 
          @click="deleteJob(job.id)" 
          class="inline-flex items-center px-3 py-2 text-sm font-medium text-red-700 bg-red-50 border border-red-200 rounded-md hover:bg-red-100 hover:border-red-300 transition-colors duration-200"
        >
          Delete
        </button>
      </div>
    </div>
  </div>
</template>