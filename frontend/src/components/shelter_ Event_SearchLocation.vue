<template>
    <div class="relative">
        <button @click="toggleDropdown">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512" width="25" height="25">
                <path fill="#f03d3d"
                    d="M172.3 501.7C27 291 0 269.4 0 192 0 86 86 0 192 0s192 86 192 192c0 77.4-27 99-172.3 309.7-9.5 13.8-29.9 13.8-39.5 0zM192 272c44.2 0 80-35.8 80-80s-35.8-80-80-80-80 35.8-80 80 35.8 80 80 80z" />
            </svg>
        </button>
        <div class="absolute -top-3 right-7 w-[22rem] rounded-md" v-if="showDropdown">
            <div class="w-full p-2">
                <div class="relative">
                    <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3">
                        <MagnifyingGlassIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
                    </div>
                    <input id="search" name="search"
                        class="block w-full rounded-md bg-white py-1.5 pl-10 pr-3 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-teal-600 sm:text-sm sm:leading-6"
                        placeholder="Search Location" type="search" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { MagnifyingGlassIcon } from '@heroicons/vue/24/outline'

export default {
    components: { MagnifyingGlassIcon },
    data() {
        return {
            showDropdown: false
        }
    },
    methods: {
        toggleDropdown() {
            this.showDropdown = !this.showDropdown
        }
    }
}
</script>