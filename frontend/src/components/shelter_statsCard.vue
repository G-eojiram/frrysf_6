<template>
    <div>
        <dl
            class="grid grid-cols-1 divide-y divide-gray-200 overflow-hidden rounded-lg bg-white shadow md:grid-cols-3 md:divide-x md:divide-y-0">
            <div v-for="item in stats" :key="item.name" class="px-4 py-5 sm:p-6">
                <dt class="text-base font-medium text-gray-600">{{ item.name }}</dt>
                <dd class="mt-1 flex items-baseline justify-between md:block lg:flex">
                    <div class="flex items-baseline text-3xl font-semibold"
                        :class="[item.name === 'Reports' ? 'text-red-500' : item.name === 'Chats' ? 'text-green-500' : item.name === 'Re-homed Pets' ? 'text-amber-500' : 'text-gray-500']">
                        {{ item.stat }}
                    </div>

                    <div>
                        <component :is="item.icon" class="h-7 w-7"
                            :class="[item.name === 'Reports' ? 'text-gray-500' : item.name === 'Chats' ? 'text-green-600' : item.name === 'Re-homed Pets' ? 'text-teal-500' : 'text-gray-600']" />
                    </div>
                </dd>
            </div>
        </dl>
    </div>
</template>

<script setup>
import { ChatBubbleBottomCenterTextIcon, HomeModernIcon, NewspaperIcon } from '@heroicons/vue/20/solid'

const stats = [
    { name: 'Reports', stat: '0', icon: NewspaperIcon },
    { name: 'Re-homed Pets', stat: '0', icon: HomeModernIcon },
    { name: 'Chats', stat: '0', icon: ChatBubbleBottomCenterTextIcon },
]
</script>