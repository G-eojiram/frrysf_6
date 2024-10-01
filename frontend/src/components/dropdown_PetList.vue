<template>
  <div class="flex flex-col">
    <label for="AnimalProfiles" class="block text-sm font-medium leading-6 text-gray-700">Animal
      Profiles</label>
    <select id="AnimalProfiles" name="AnimalProfiles" @change="$emit('select', $event.target.value)"
      class="mt-2 block w-full rounded-md border-0 py-2 pl-[1rem] pr-10 text-gray-800 ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-black sm:text-sm sm:leading-6 leading-relaxed">
      <option value="" selected disabled hidden>Select Animal Profile</option>
      <option v-for="(option, index) in options" :key="index" :value="option.id">
        {{ option.name }}
      </option>
    </select>
  </div>
</template>
<script>
export default {
  data() {
    return {
      options: [
        {
          id: 1,
          name: 'Eric',
          rehomed: 'sept 23123',
          breed: 'dogunkwon'
        },
        {
          id: 2,
          name: 'Chellsey',
          rehomed: 'sept 23123',
          breed: 'dogunkwon'
        },
        {
          id: 3,
          name: 'Jeneh',
          rehomed: 'sept 23123',
          breed: 'dogunkwon'
        },
        {
          id: 4,
          name: 'Cyril', rehomed: 'sept 23123',
          breed: 'dogunkwon'
        },
      ]
    }
  },
  methods: {
    handleSelect(id) {
      const selectedPet = this.options.find(pet => pet.id === id);
      this.$emit('select', selectedPet);
    }
  }
  //     mounted() {
  //     axios.get('/api/options')
  //       .then(response => {
  //         this.options = response.data
  //       })
  //       .catch(error => {
  //         console.error(error)
  //       })
  //   }
}
</script>