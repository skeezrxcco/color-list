<template>
    <div class="flex-shrink-0 pr-2">
        <button type="button" @click.prevent="toggleMenu(item)"
            class=" flex items-center text-gray-400 hover:text-gray-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-indigo-500">
            <span class="sr-only">Open options</span>
            <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"
                aria-hidden="true">
                <path
                    d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z" />
            </svg>
        </button>
        <div v-show="isToggleMenu"
            class="absolute  mt-2 w-auto rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
            <div class="py-1 divide-y divide-gray-200">
                <a @click="removeCard(item)" class="text-gray-700 block px-4 py-2 text-sm cursor-pointer">🗑
                    Delete</a>
                <a @click="copyCard(item, listFull, currentList)" class="text-gray-700 block px-4 py-2 text-sm"
                    :class="[listFull ? 'cursor-not-allowed' : 'cursor-pointer']">📋
                    Copy</a>
                <a @click="move(item)" class="text-gray-700 block px-4 py-2 text-sm"
                    :class="[listTargetFull ? 'cursor-not-allowed' : 'cursor-pointer']">🏃🏼‍♂️💨 Move</a>
                <a @click="reference()" class="text-gray-700 block px-4 py-2 text-sm cursor-help">🎨
                    Reference</a>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    emits: ['removeCard', 'copyCard', 'move', 'reference','toggleMenu'],
    props: {
        isToggleMenu: Boolean,
        listFull: Boolean,
        listTargetFull: Boolean,
        item: Object,
        currentList: Number
    },
    methods: {
        removeCard(item) {
            this.$emit('removeCard', item)
        },
        copyCard(item, listFull, currentList) {
            this.$emit('copyCard', item, listFull, currentList)
        },
        move(item) {
            this.$emit('move', item)
        },
        reference() {
            this.$emit('reference')
        },
        toggleMenu(item){
            this.$emit('toggleMenu',item)
        }
    }

}
</script>
// Props: item.toggleMenu, :listFull= listOneFull, :listTarget = ListTwoFull