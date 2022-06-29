<template>
    <div class="col-span-1 flex shadow-sm rounded-md mb-2">
        <div
            class="flex-shrink-0 flex items-center justify-center w-16 bg-pink-600 text-white text-sm font-medium rounded-l-md">
        </div>
        <div
            class="flex-1 flex items-center justify-between border-t border-r border-b border-gray-200 bg-white rounded-r-md truncate">
            <div class="flex-1 px-4 py-2 text-base truncate">
                <a href="#" class="text-gray-900 font-medium hover:text-gray-600">Pink</a>
                <p class="text-gray-500 text-sm">16 Members</p>
            </div>
            <div class="flex-shrink-0 pr-2">
                <button type="button"
                    class=" flex items-center text-gray-400 hover:text-gray-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-indigo-500"
                    id="menu-button" aria-expanded="true" aria-haspopup="true">
                    <span class="sr-only">Open options</span>
                    <!-- Heroicon name: solid/dots-vertical -->
                    <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"
                        aria-hidden="true">
                        <path
                            d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z" />
                    </svg>
                </button>
                <div v-show="true"
                    class="absolute  mt-2 w-auto rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                    role="menu" aria-orientation="vertical" aria-labelledby="menu-button" tabindex="+1">
                    <div class="py-1" role="none">
                        <!-- Active: "bg-gray-100 text-gray-900", Not Active: "text-gray-700" -->
                        <a href="#" class="text-gray-700 block px-4 py-2 text-sm" role="menuitem" tabindex="-1"
                            id="menu-item-0">🗑 Delete</a>
                        <a href="#" class="text-gray-700 block px-4 py-2 text-sm" role="menuitem" tabindex="-1"
                            id="menu-item-1">📋 Copy</a>
                        <a href="#" class="text-gray-700 block px-4 py-2 text-sm" role="menuitem" tabindex="-1"
                            id="menu-item-2">🏃🏼‍♂️💨 Move</a>
                        <a href="#" class="text-gray-700 block px-4 py-2 text-sm" role="menuitem" tabindex="-1"
                            id="menu-item-2">🎨 Reference</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>