<template>
    <TransitionRoot as="template" :show="open">
        <Dialog as="div" class="relative z-30" @close="open = false">
            <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100"
                leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
                <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
            </TransitionChild>
            <div class="fixed inset-0 z-10 overflow-y-auto">
                <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
                    <TransitionChild as="template" enter="ease-out duration-300"
                        enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                        enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200"
                        leave-from="opacity-100 translate-y-0 sm:scale-100"
                        leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
                        <DialogPanel
                            class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-[36.5rem] sm:p-6">
                            <div class="sm:flex sm:items-start">
                                <div class="mt-3 text-center sm:mt-0 sm:text-left w-full">
                                    <div class="flex justify-end">
                                        <button @click="open = false" ref="cancelButtonRef">
                                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                                                stroke="currentColor" stroke-width="2" class="w-4 h-4">
                                                <path stroke-linecap="round" stroke-linejoin="round"
                                                    d="M6 18L18 6M6 6l12 12" />
                                            </svg>
                                        </button>
                                    </div>
                                    <DialogTitle as="h3"
                                        class="mb-[1.5rem] text-2xl font-semibold leading-6 text-gray-700 flex justify-center">
                                        Report Post
                                    </DialogTitle>
                                    <div
                                        class="overflow-hidden sm:mx-0 md:mx-4 xl:mx-4">
                                        <div class="flex gap-x-1 text-sm text-gray-400 py-2">
                                            <label for="location">Location:</label>
                                            <input type="text" id="location" placeholder="Enter Location"
                                                class="outline-none w-full">
                                        </div>
                                        <div class="mt-1 border rounded-lg border-gray-200">
                                            <label for="caption" class="sr-only">Report Caption</label>
                                            <textarea v-model="caption" name="caption" id="caption"
                                                placeholder="Write a caption or description of this Report ..."
                                                class="py-[10px] px-6 w-full h-[8rem] focus:outline-none" />
                                        </div>
                                        <div class="flex justify-between my-3 mx-[1.5rem]">
                                            <div>
                                                <span class="text-gray-400 text-[12px]">Add to your post</span>
                                            </div>
                                            <div class="flex gap-4 items-center">
                                                <div>
                                                    <label for="file-input"
                                                        class="cursor-pointer flex gap-3 items-center">
                                                        <input type="file" multiple @change="handleFileChange"
                                                            id="file-input" ref="fileInput" class="hidden" />
                                                        <img :src="images" alt="Images Icon"
                                                            class="h-[2rem] w-[2rem]" />
                                                    </label>
                                                </div>
                                                <div>
                                                    <!-- logic sa location map pin?? ah basta mao ni icon na button -->
                                                    <button type="button">
                                                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512"
                                                            width="25" height="25">
                                                            <path fill="#f03d3d"
                                                                d="M172.3 501.7C27 291 0 269.4 0 192 0 86 86 0 192 0s192 86 192 192c0 77.4-27 99-172.3 309.7-9.5 13.8-29.9 13.8-39.5 0zM192 272c44.2 0 80-35.8 80-80s-35.8-80-80-80-80 35.8-80 80 35.8 80 80 80z" />
                                                        </svg>
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="px-[2rem] py-[1rem]">
                                        <div v-if="imageUrls.length > 0" class="grid grid-cols-4 gap-2">
                                            <div v-for="(imageUrl, index) in imageUrls" :key="index" class="relative">
                                                <img :src="imageUrl" alt="Uploaded Image"
                                                    class="max-w-[100px] max-h-[100px] object-contain border" />
                                                <button @click="removeImage(index)"
                                                    class="absolute top-0 right-0 p-1 text-gray-500 hover:text-gray-800">
                                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                                                        fill="none" stroke="currentColor" stroke-width="2"
                                                        class="w-4 h-4">
                                                        <path stroke-linecap="round" stroke-linejoin="round"
                                                            d="M6 18L18 6M6 6l12 12" />
                                                    </svg>
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="flex justify-center">
                                <button type="button"
                                    class="inline-flex w-full justify-center rounded-md bgteal px-[12.2rem] py-2 text-sm font-semibold text-white shadow-sm hover:bg-bgteal sm:ml-3 sm:w-auto"
                                    @click="open = false">Post</button>
                            </div>
                        </DialogPanel>
                    </TransitionChild>
                </div>
            </div>
        </Dialog>
    </TransitionRoot>
</template>
<script>
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import searchlocation from '@/components/shelter_ Event_SearchLocation.vue'

export default {
    components: { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot, searchlocation },
    data() {
        return {
            open: true,
            fileInput: null,
            imageUrls: [],
            images: 'https://img.icons8.com/fluency/48/stack-of-photos.png',
            startDateTime: '',
            endDateTime: '',
        }
    },
    methods: {
        handleFileChange(event) {
            const files = event.target.files;
            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                const reader = new FileReader();
                reader.onload = (event) => {
                    this.imageUrls.push(event.target.result);
                };
                reader.readAsDataURL(file);
            }
        },
        removeImage(index) {
            this.imageUrls.splice(index, 1);
        },
    }
}
</script>