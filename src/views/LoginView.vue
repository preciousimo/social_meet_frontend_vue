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
                <form class="space-y-6" v-on:submit.prevent="submitForm"> 
                    <div>
                        <label for="email" class="block mb-2 text-sm font-medium text-gray-600">Email</label>
                        <input type="email" v-model="form.email" placeholder="Your e-mail address" id="email" class="w-full px-4 py-2 border border-gray-300 rounded-lg appearance-none focus:outline-none focus:border-gray-600">
                    </div>

                    <div>
                        <label for="password" class="block mb-2 text-sm font-medium text-gray-600">Password</label>
                        <input type="password" v-model="form.password" placeholder="Your password" id="password" class="w-full px-4 py-2 border border-gray-300 rounded-lg appearance-none focus:outline-none focus:border-gray-600">
                    </div> 

                    <template v-if="errors.length > 0">
                        <div class="bg-red-300 text-white rounded-lg p-6">
                            <p v-for="error in errors" v-bind:key="error">{{ error }}</p>
                        </div>
                    </template>

                    <div>
                        <button type="submit" class="w-full px-4 py-2 text-lg font-semibold text-white transition-colors duration-300 bg-purple-800 rounded-lg hover:bg-purple-700 focus:outline-none focus:bg-gray-700">Log in</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { useUserStore } from '@/stores/user'
export default {
    setup() {
        const userStore = useUserStore()
        return {
            userStore
        }
    },
    data() {
        return {
            form: {
                email: '',
                password: '',
            },
            errors: []
        }
    },
    methods: {
        async submitForm() {
            this.errors = []
            if (this.form.email === '') {
                this.errors.push('Your e-mail is missing')
            }
            if (this.form.password === '') {
                this.errors.push('Your password is missing')
            }
            if (this.errors.length === 0) {
                await axios
                    .post('/api/login/', this.form)
                    .then(response => {
                        this.userStore.setToken(response.data)
                        console.log(response.data.access)
                        axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.access;
                    })
                    .catch(error => {
                        console.log('error', error)
                    })
                
                await axios
                    .get('/api/me/')
                    .then(response => {
                        this.userStore.setUserInfo(response.data)
                        this.$router.push('/feed')
                    })
                    .catch(error => {
                        console.log('error', error)
                    })
            }
        }
    }
}
</script>
