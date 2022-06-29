<template>
  <div
    class="border border-gray-200 rounded-lg shadow-sm divide-y divide-gray-200"
  >
    <!-- List Header -->
    <div
      class="relative bg-gray-200 px-6 py-2 shadow-sm flex items-center space-x-3"
    >
      <div class="flex-1 min-w-0">
        <a href="#" class="focus:outline-none">
          <span class="absolute inset-0" aria-hidden="true"></span>
          <p class="text-lg font-medium text-gray-900">Board # 1</p>
        </a>
      </div>
      <div class="flex-shrink-0">
        <button
          type="button"
          class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
        >
          <!-- Heroicon name: solid/plus-sm -->
          <svg
            class="h-5 w-5"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            fill="currentColor"
            aria-hidden="true"
          >
            <path
              fill-rule="evenodd"
              d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
      </div>
    </div>
    <!-- Card -->
    <ListItem />
  </div>
</template>
<script>
import ListItem from './ListItem/ItemIndex.vue'
export default {
    components:{
      ListItem
    }
}
</script>

