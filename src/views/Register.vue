<template>
<div class="max-w-screen-sm mx-auto px-4 py-10">

<!-- Register -->
<form
@submit.prevent="register"
class="p-8 flex-col bg-grey rounded-md shadow-1g">
<h1 class="text-3xl text-deep-green mb-4">Register</h1>

<div class="flex-col mb-2">
<label for="email" class="mb-1 text-sm text-deep-green">Email</label>
<input type="text"
required
class="p-2 text-gray-500 focus:outline-none"
id="email"
v-model="email">
</div>

<div class="flex-col mb-2">
<label for="password" class="mb-1 text-deep-green">password</label>
<input type="text"
required
class="p-2 text-gray-500 focus:outline-none"
id="password"
v-model="password">
</div>

<div class="flex-col mb-2">
<label for="confirmPassword" class="mb-1 text-sm text-deep-green">confirmPasseord</label>
<input type="text"
required
class="p-2 text-grey-500 focus:outline-none"
id="confirmPassword"
v-model="confirmPassword"
>
</div>

<button type="submit" @click="register" class="mt-6 py-6 rounded-sm self-start text-sm
text-white bg-deep-green duration-200 border-2 border-transparent hover:border-deep-green hover:bg-white
hover:text-deep-green">Register</button>

<router-link class="text-sm mt-6 text-center" :to="{name: 'Login'}">
Already have an account? <span class="text-deep-green ">Login</span>
</router-link>
</form>
</div>
</template>

<script>
import {ref} from "vue"
import {supabase} from "./supabase"
import {useRouter} from "vue-router"

export default {
name: "register",
component:{},
setup() {
    const router = useRouter()
    const email = ref(null)
    const password = ref(null)
    const confirmPassword = ref(null)
    const errorMsg = ref(null)

    const register = async () => {
        if (password.value === confirmPassword.value){
            try {
                const {error} = await supabase.auth.signUp({
                    email: email.value,
                    password: password.value
                })
                if (error) throw error
                    console.log("click")
                router.push({name:"Login"})
            }   catch(error){
                errorMsg.value = error.message
            } 
        }
        errorMsg.value = "Error: Password do not match"
        setTimeout(() => {
            errorMsg.value = null
        }, 5000)
    }
    
    return{ email, password, confirmPassword, errorMsg, register}
}
}
</script>