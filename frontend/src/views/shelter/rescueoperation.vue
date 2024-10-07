<script>
import textvalue from '@/components/textString.vue'
import datetoday from '@/components/dateCard.vue'
import linkfooter from '@/components/footerLink.vue'
import reports from '@/components/shelter_ReportsCard.vue'
import chats from '@/components/shelter_RescueOp_ChatBox.vue'

export default {
    components: {
        textvalue, datetoday, linkfooter, reports, chats
    },
};
</script>
<template>
    <div class="h-screen flex flex-col">
        <header class="flex justify-between items-center">
            <div class="graycolor">
                <textvalue msg="Rescue Operation" />
            </div>
            <div class="flex gap-5">
                <datetoday />
            </div>
        </header>
        <main class="mt-[1rem]">
            <div class="flex gap-6 h-full">
                <div class="border rounded-lg w-[30%] bg-slate-50">
                    <div class="flex items-center gap-3 px-[1.5rem] py-[.5rem] bg-white border-b-2 rounded-t-lg">
                        <img width="30" height="30"
                            src="https://img.icons8.com/glyph-neue/64/4D4D4D/push-notifications.png"
                            alt="push-notifications" />
                        <span class="graycolor text-sm font-semibold">Reports Feed</span>
                    </div>
                    <div class="overflow-y-scroll h-[50rem] p-[1rem]">
                        <reports />
                    </div>
                </div>
                <div class="border rounded-lg w-[70%] h-full bg-gray-50">
                    <!-- <div class="flex items-center gap-3 px-[1.5rem] py-[.5rem] bg-white border-b-2 rounded-t-lg">
                        <img width="30" height="30"
                            src="https://img.icons8.com/glyph-neue/64/4D4D4D/push-notifications.png"
                            alt="push-notifications" />
                        <span class="graycolor text-sm font-semibold">Reports Feed</span>
                    </div> -->
                    <div class="h-[50rem]">
                        <chats />
                    </div>

                </div>
            </div>
        </main>
        <footer class="mt-auto">
            <linkfooter />
        </footer>
    </div>
</template>