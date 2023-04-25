<template>

    <div class="max-w-screen-md mx-auto px-4 py-10" >
        <!-- ststus Message -->

        <div v-if="statusMsg || errorMSg" class="mb-10 p-4 bg gray-400 rounded-md">
            <p class="text-gray-400" >{{statusMsg}}</p>
            <p class="text-red-500">{{errorMsg}}</p>
        </div>

        <!-- create -->
        <div class="p-8 flex flex-col items-start bg-gray-100 rounded-md shadow-lg ">
        <form  @submit.prevent="createWorkout" class="flex-col gap-y-5 w-full  p-2">
            <h1 class="text-2xl text-light-green">Generate Day</h1>

        <!-- workout day -->
        <label for="workout-name" class="mb-1 text-sm text-my-green" > Excersise Day </label>
        <div class="flex-col">
            <input 
            type="text"
            required
            class="p-2 mt-2 text-gray-500 focus:outline-my-cyan"
            id="workout-name"
            v-model="excersiseDay">
        </div>

         <!-- workout date -->
        <label for="workout-date" class="mt-1 mb-1 text-sm text-my-green"> Date</label>
        <div class="flex-col">

            <input 
            type="date"
            required
            class="p-2 mt-2 text-gray-500 focus:outline-my-cyan"
            id="workout-date"
            v-model="workoutDate">
        </div>

            <button  type="submit" class="bg-blue-light rounded-md text-deep-green p-4 m-1 mt-4 flex-col border-deep-green
            hover:bg-grey-500 border-my-cyan hover:bg-white">Save</button>
        </form>

        </div>
    </div>
</template>

<script>
import { PlusIcon } from "@vue-hero-icons/outline"
import {ref, computed} from "vue"
import {uid} from "uid"
import {supabase} from "./supabase.js"
import store from '../store.js'
export default {
    name: 'Generate',
            setup() {
                const workoutDate = ref(null)
                const excersiseDay = ref('')
                const statusMsg = ref(null)
                const errorMsg = ref(null)
                const user = computed(() =>store.state.user)
                
        // create excersises
        const createWorkout = async () => {
            try{
                const {error} = await supabase.from ("activityDay").insert([
                    { 
                        workoutDate: workoutDate.value,
                        excersiseDay: excersiseDay.value
                    },
                ])
                console.log('workout')
                if (error) throw error

                statusMsg.value = "Day Created"
                excersiseDay.value = null
                workoutDate.value = null

            }catch(error){
                errorMsg.value = `Error: ${error.message}`
                setTimeout(() =>{
                    errorMsg.value = false
                    },5000)
            }
        }
    return{ createWorkout, workoutDate, excersiseDay, statusMsg, errorMsg}
    }
}
</script>