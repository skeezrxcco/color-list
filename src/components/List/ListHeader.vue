<template>
    <div class="relative  bg-gray-200 px-6 py-2 shadow-sm flex items-center space-x-3 ">
        <div class="flex-1 min-w-0">
            <p class="text-lg font-medium text-gray-900">Board # {{currentList}} </p>
        </div>
        <div class="flex-shrink-0">
            <button v-show="selectedCard&&item.listId ==currentList" @click="removeCard(item)" class=" mr-2 inline-flex items-center p-1 border border-transparent 
                rounded-full shadow-sm text-white bg-red-800 hover:bg-red-600 
                focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500">
                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" fill="#000000" viewBox="0 0 24 24" width="24px"
                    height="24px">
                    <path
                        d="M 10 2 L 9 3 L 4 3 L 4 5 L 20 5 L 20 3 L 15 3 L 14 2 L 10 2 z M 5 7 L 5 20 C 5 21.1 5.9 22 7 22 L 17 22 C 18.1 22 19 21.1 19 20 L 19 7 L 5 7 z M 8 9 L 10 9 L 10 20 L 8 20 L 8 9 z M 14 9 L 16 9 L 16 20 L 14 20 L 14 9 z" />
                </svg>
            </button>
            <button @click="addCard(currentList)" :disabled="listFull"  class="inline-flex items-center p-1 border border-transparent 
                rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 
                focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">

                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"
                    aria-hidden="true">
                    <path fill-rule="evenodd"
                        d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z"
                        clip-rule="evenodd" />
                </svg>
            </button>
        </div>
    </div>
</template>
<script>
export default {
    emits: ['removeCard', 'addCard'],
    props: {
        selectedCard: Number,
        listFull: Boolean,
        listTargetFull: Boolean,
        currentList: Number,
        item: Object,
    },
    methods: {
        addCard(currentList){
            this.$emit('addCard',currentList)
        },
        removeCard(item){
            
            this.$emit('removeCard',item)
        }
    }
}
</script>