<script setup lang="ts">
import AxiosInstance from '@/lib/axios';
import { reactive } from 'vue';

interface RegisterForm {
    name: string;
    email: string;
    password: string;
    password_confirmation: string;
}

const form = reactive<RegisterForm>({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
});

const register = async (payload: RegisterForm) => {
    await AxiosInstance.get("/sanctum/csrf-cookie", {
        baseURL: "http://localhost:8000",
    })
    try {
        const response = await AxiosInstance.post('/register', payload);
        console.log(response.data)
    } catch (error) {
        console.error(error)
    }
};


</script>
<template>
    <h1 class="text-3xl text-slate-200 p-4">Register</h1>
    <form class="max-w-sm p-4 rounded-lg shadow-md bg-stay-900" @submit.prevent="register(form)">
        <div class="mb-5 p-4">
            <label for="name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Name</label>
            <input v-model="form.name" type="name" id="name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="name" />
        </div>
        <div class="mb-5 p-4">
            <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Email</label>
            <input v-model="form.email" type="email" id="email" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="name@flowbite.com"  />
        </div>
        <div class="mb-5 p-4">
            <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
            <input v-model="form.password" type="password" id="password" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" />
        </div>
        <div class="mb-5 p-4">
            <label for="password_confirmation" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password confirmation</label>
            <input v-model="form.password_confirmation" type="password_confirmation" id="password" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" />
        </div>
        <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Submit</button>
    </form>
</template>