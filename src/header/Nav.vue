<script>
export default {
    methods: {
        
    },
}
</script>

<template>
    <nav class="border-gray-200 bg-gray-600 dark:bg-gray-800 dark:border-gray-700">
        <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
            <div class="flex items-center space-x-3 rtl:space-x-reverse">
                <img src="./../../public/pokeball.png" class="h-8" alt="Flowbite Logo" />
                <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">Pokedex</span>
            </div>
            <button data-collapse-toggle="navbar-hamburger" type="button" class="inline-flex items-center justify-center p-4 w-24 h-12 text-sm text-gray-500 rounded-lg focus:outline-none  dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600" aria-controls="navbar-hamburger" aria-expanded="false">
                <img src="./../../public/gotcha.png" alt="">
                <span class="text-white">List</span>
            </button>
            <div class="hidden w-full" id="navbar-hamburger">
            <ul class="flex flex-col font-medium mt-4 rounded-lg bg-gray-50 dark:bg-gray-800 dark:border-gray-700">
                <li>
                
                </li>
            </ul>
            </div>
        </div>
    </nav>
</template>

<style>

</style>