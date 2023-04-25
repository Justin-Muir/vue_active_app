<template>
    <div class="max-w-screen-sm mx-auto px-4 py-10">

        <!-- register -->
        <form class="p-8 flex-col bg-light-grey rounded-md shadow-2xl" @submit.prevent>
            <h1 class="text-3xl text-deep-green mb-4 " >Login</h1>

            <div class="flex-col mb-2">
                <label for="email" class="mb-1 text-sm text-deep-green px-4">Email</label>
                <input type="text"
                required
                class="p-2 text-gray-500 focus:outline-none"
                id="email"
                v-model="email">
            </div>

            <div class="flex-col mb-2">
                <label for="password" class="mb-1 text-sm text-deep-green px-4">password </label>
                <input type="text"
                required
                class="p-2 text-gray-500 focus:outline-none "
                id="password"
                v-model="password">
            </div>

            <button type="submit" @click="login" class="mt-6 py-2 px-6 rounded-md self-start text-sm
            text-deep-green bg-blue-light duration-200 border-solid border-2 border-transparent hover:border-deep-green hover:my-green"
            > Login </button>
        </form>
    </div>
</template>

<script>
import {ref} from "vue"
import {supabase} from "./supabase"
import {useRouter} from "vue-router"

export default{
    name: "Login",
    setup(){
        const router = useRouter()
        const email = ref(null)
        const password = ref(null)
        const errorMsg = ref(null)

        const login = async () => {
            const {error} = await supabase.auth.signInWithPassword({
                email: email.value,
                    password: password.value,
                })
                try{
                if(error) throw error
                console.log(errorMsg.value)
                router.push({name: "Home"})
                console.log('go true')
            } catch (error){
                errorMsg.value = `Error: ${error.message}` 
                setTimeout(() => {
                    errorMsg.value = null
                },5000)
            }
        }
     return {email, password, errorMsg, login}
    }
}
</script>