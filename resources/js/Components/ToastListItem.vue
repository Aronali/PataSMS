<script setup>

const props = defineProps({
    message: String,
    type: String,
    duration: {
        type: Number,
        default: 8000,
    }
})

const emit = defineEmits(['remove'])

setTimeout(() => {
    emit('remove')
}, props.duration)
</script>

<template>
    <div class="shadow-sm border md:border-0 border-gray-100 rounded-lg bg-white mx-auto m-8 p-4 w-full flex" role="alert">
        <div class="pr-2" v-if="type === 'error' || type === 'Error' || type === 'ERROR'">
            <svg
                class="fill-current text-red-600"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                width="24"
                height="24"
            >
                <path
                    class="heroicon-ui"
                    d="M12 2a10 10 0 1 1 0 20 10 10 0 0 1 0-20zm0 2a8 8 0 1 0 0 16 8 8 0 0 0 0-16zm0 9a1 1 0 0 1-1-1V8a1 1 0 0 1 2 0v4a1 1 0 0 1-1 1zm0 4a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"
                />
            </svg>
        </div>
        <div v-else-if="type === 'success' || type === 'Success' || type === 'SUCCESS'" class="pr-2">
            <svg
                class="fill-current text-green-600"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                width="22"
                height="22"
            >
                <path
                    class="heroicon-ui"
                    d="M12 22a10 10 0 1 1 0-20 10 10 0 0 1 0 20zm0-2a8 8 0 1 0 0-16 8 8 0 0 0 0 16zm-3.54-4.46a1 1 0 0 1 1.42-1.42 3 3 0 0 0 4.24 0 1 1 0 0 1 1.42 1.42 5 5 0 0 1-7.08 0zM9 11a1 1 0 1 1 0-2 1 1 0 0 1 0 2zm6 0a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"
                />
            </svg>
        </div>
        <div v-else-if="type === 'warning' || type === 'Warning' || type === 'WARNING'" class="pr-2">
            <svg
                class="fill-current text-orange-600"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                width="24"
                height="24"
            >
                <path
                    class="heroicon-ui"
                    d="M12 2a10 10 0 1 1 0 20 10 10 0 0 1 0-20zm0 2a8 8 0 1 0 0 16 8 8 0 0 0 0-16zm0 9a1 1 0 0 1-1-1V8a1 1 0 0 1 2 0v4a1 1 0 0 1-1 1zm0 4a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"
                />
            </svg>
        </div>
        <div v-else class="pr-2">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" width="24" height="24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M11.25 11.25l.041-.02a.75.75 0 011.063.852l-.708 2.836a.75.75 0 001.063.853l.041-.021M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-9-3.75h.008v.008H12V8.25z" />
            </svg>
        </div>

        <div class="w-full">
            <div class="text-sm pb-2">
                {{ type ?? 'info' }}
                <span class="float-right p-1 rounded-2xl focus:ring-2 focus:ring-gray-100 hover:bg-gray-50" @click="emit('remove')">
              <svg
                  class="fill-current text-gray-600"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  width="22"
                  height="22"
              >
                <path
                    class="heroicon-ui"
                    d="M16.24 14.83a1 1 0 0 1-1.41 1.41L12 13.41l-2.83 2.83a1 1 0 0 1-1.41-1.41L10.59 12 7.76 9.17a1 1 0 0 1 1.41-1.41L12 10.59l2.83-2.83a1 1 0 0 1 1.41 1.41L13.41 12l2.83 2.83z"
                />
              </svg>
            </span>
            </div>
            <div class="text-sm text-gray-600  tracking-tight ">
               {{ message ?? '-' }}
            </div>
        </div>
    </div>

</template>
