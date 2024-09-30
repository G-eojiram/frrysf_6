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
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <div class="sm:flex sm:items-start">
                <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left">
                  <div class="flex justify-end">
                    <button @click="open = false" ref="cancelButtonRef">
                      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                        stroke-width="2" class="w-4 h-4">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                      </svg>
                    </button>
                  </div>
                  <DialogTitle as="h3"
                    class="mb-[1.5rem] text-[1.3rem] font-semibold leading-6 text-gray-700 flex justify-center">
                    Create New Post
                  </DialogTitle>
                  <div>
                    <!-- ref="petList" -->
                    <PetList @select="handleSelectPetList" />
                  </div>
                  <!-- v-if="selectedPetId" to display the details and get the id-->
                  <div class="mt-4 border rounded-lg">
                    <div v-if="selectedPetId" class="text-sm mt-1.5">
                      <div class="flex flex-col">
                        <label for="petName" class="px-6 font-medium text-sm leading-6 text-gray-400">
                          Name</label>
                        <div class="mt-1.5 border-y flex items-center pl-6">
                          <img width="30" height="30"
                            src="https://img.icons8.com/sf-black-filled/30/8E8E8E/cat-footprint.png"
                            alt="cat-footprint" />
                          <input type="text" name="petName" id="petName" placeholder="petname" v-model="petName"
                            class="p-1.5 ml-2 px-2 w-full" readonly>
                        </div>
                      </div>
                      <div class="flex flex-col mt-1.5">
                        <label for="rehomed" class="px-6 font-medium text-sm leading-6 text-gray-400">
                          Date Re-homed</label>
                        <div class="mt-1.5 border-y flex items-center pl-6">
                          <img width="30" height="30"
                            src="https://img.icons8.com/external-jumpicon-glyph-ayub-irawan/30/8E8E8E/external-pet-real-estate-jumpicon-glyph-jumpicon-glyph-ayub-irawan.png"
                            alt="external-pet-real-estate-jumpicon-glyph-jumpicon-glyph-ayub-irawan" />
                          <input type="text" name="rehomed" id="rehomed" placeholder="rehomed" v-model="rehomed"
                            class="p-1.5 ml-2 px-2 w-full" readonly>
                        </div>
                      </div>
                      <div class="flex flex-col mt-1.5">
                        <label for="petBreed" class="px-6 font-medium text-sm leading-6 text-gray-400">
                          Breed / Mix</label>
                        <div class="mt-1.5 border-y flex items-center pl-7">
                          <img width="25" height="25"
                            src="https://img.icons8.com/external-basicons-solid-edtgraphics/25/8E8E8E/external-question-ui-edtim-solid-edtim.png"
                            alt="external-question-ui-edtim-solid-edtim" />
                          <input type="text" name="petBreed" id="petBreed" placeholder="petbreed" v-model="petBreed"
                            class="p-1.5 ml-2 px-3 w-full" readonly>
                        </div>
                      </div>
                    </div>
                    <div>
                      <textarea v-model="newpost" placeholder="Write a caption or description of this post..."
                        name="postcaption" id="postcaption" class="py-[1rem] px-6 w-[27rem] h-[8rem] text-md" />
                    </div>
                  </div>
                  <div class="px-[2rem] py-[1rem]">
                    <div class="flex justify-between mb-3">
                      <span class="text-gray-400 text-[14px]">Add to your post</span>
                      <label for="file-input" class="cursor-pointer flex gap-3 items-center">
                        <input type="file" multiple @change="handleFileChange" id="file-input" ref="fileInput"
                          class="hidden" />
                        <img :src="images" alt="Images Icon" class="h-[2rem] w-[2rem]" />
                      </label>
                    </div>
                    <div v-if="imageUrls.length > 0" class="grid grid-cols-4 gap-2">
                      <div v-for="(imageUrl, index) in imageUrls" :key="index" class="relative">
                        <img :src="imageUrl" alt="Uploaded Image"
                          class="max-w-[100px] max-h-[100px] object-contain border" />
                        <button @click="removeImage(index)"
                          class="absolute top-0 right-0 p-1 text-gray-500 hover:text-gray-800">
                          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2" class="w-4 h-4">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                          </svg>
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="flex justify-center">
                <button type="button"
                  class="inline-flex w-full justify-center rounded-md bgteal px-[12.2rem] py-2 text-sm font-semibold text-white shadow-sm hover:bg-bgteal sm:ml-3 sm:w-auto">
                  Post</button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
<script>
import { ref } from 'vue'
import PetList from '@/components/dropdown_PetList.vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'

export default {
  components: { PetList, Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot, },
  data() {
    return {
      open: true,
      fileInput: null,
      imageUrls: [],
      images: 'https://img.icons8.com/fluency/48/stack-of-photos.png',
      // for petlist
      selectedPetId: null,
      petName: '',
      rehomed: '',
      petBreed: '',
      newpost: '',
    }
  },
  methods: {
    // handleSelectPetList(id) {
    //   const selectedPet = this.$refs.petList.options.find(pet => pet.id === id);
    //   if (selectedPet) {
    //     this.selectedPetId = id;
    //     this.petName = selectedPet.name;
    //     this.rehomed = selectedPet.rehomed;
    //     this.petBreed = selectedPet.breed;
    //     console.log(`Selected pet ID: ${this.selectedPetId}`);
    //   } else {
    //     console.log("No pet found with that ID");
    //   }
    // },

    handleSelectPetList(id) {
      this.selectedPetId = id;
      console.log(`Selected pet ID: ${id}`);
    },
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
    // handleSubmit() {
    //   // Use the newpost property to submit the entered text
    //   console.log(this.newpost);
    //   // Submit the text to a server or perform further processing
    // }
  }
}
</script>