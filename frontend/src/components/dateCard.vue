<script>
import { CalendarDaysIcon } from '@heroicons/vue/24/outline'
export default {
  components: { CalendarDaysIcon },
  computed: {
    getCurrentDate() {
      const date = new Date();
      const month = date.toLocaleString('default', { month: 'long' });
      const day = date.getDate();
      return `${month} ${day}`;
    },
    getDay() {
      const date = new Date();
      const day = date.toLocaleString('default', { weekday: 'long' });
      return day;
    }
  },
};
</script>
<template>
  <div
    class="border bg-slate-50 rounded-md p-[5px] sm:px-3 px-5 space-x-2 text-[10px] flex items-center lightgraycolor">
    <div class="flex items-center">
      <CalendarDaysIcon class="w-5" />
      <div class="ml-2 graycolor font-bold sm:text-[11px] pr-2">Today</div>
      <div class="ml-auto graycolor font-medium sm:text-[11px]">
        {{ getCurrentDate }} | {{ getDay }}
      </div>
    </div>
  </div>
</template>