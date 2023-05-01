<template>
    <div class="max-w-7xl mx-auto grid grid-cols-2 gap-4">
        <div class="main-left">
            <div class="p-12 bg-white border border-gray-200 rounded-lg">
                <h1 class="mb-6 text-2xl">Log in</h1>

                <p class="mb-6 text-gray-500">
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Similique, ex aperiam minus placeat at saepe
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Similique, ex aperiam minus placeat at saepe
                </p>

                <p class="font-bold">
                    Don't have an account? <RouterLink :to="{'name': 'signup'}" class="underline">Click here</RouterLink> to create one.
                </p>
            </div>
        </div>

        <div class="main-right">
            <div class="p-12 bg-white border border-gray-200 rounded-lg">
                <form class="space-y-6"> 
                    <div>
                        <label for="email" class="block mb-2 text-sm font-medium text-gray-600">Email</label>
                        <input type="email" placeholder="Your e-mail address" id="email" name="email" class="w-full px-4 py-2 border border-gray-300 rounded-lg appearance-none focus:outline-none focus:border-gray-600">
                    </div>

                    <div>
                        <label for="password" class="block mb-2 text-sm font-medium text-gray-600">Password</label>
                        <input type="password" placeholder="Your password" id="password" name="password" class="w-full px-4 py-2 border border-gray-300 rounded-lg appearance-none focus:outline-none focus:border-gray-600">
                    </div> 

                    <div>
                        <button type="submit" class="w-full px-4 py-2 text-lg font-semibold text-white transition-colors duration-300 bg-purple-800 rounded-lg hover:bg-purple-700 focus:outline-none focus:bg-gray-700">Log in</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>