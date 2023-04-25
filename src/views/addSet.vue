<template>
    <div>
        
        <button class="bg-blue-light rounded-md text-deep-green w-24 border-deep-green mb-2 hover:bg-white">
            ADD SET
        </button>

        <div class="p-8 gap-3 flex flex-col flex-wrap items-start  h-full grid justify-items-center bg-gray-200 rounded-md shadow-lg">
        <form @submit.prevent="createData">
            <div>
                <label for="reps" class="mt-1 text-md text-my-green">reps</label>
                <div class="flex">
                    <input 
                    type="number"
                    class="p-2 mt-2 text-gray-500 focus:outline-my-cyan"
                    required
                    v-model="reps"
                    id="reps">
                </div>

                <label for="weights" class="mt-1 text-md text-my-green">weight</label>
                <div class="flex gap-2">
                    <input 
                    class="p-2 mt-2 text-gray-500 focus:outline-my-cyan"
                    type="number"
                    required 
                    v-model="weights"
                    id="weights">
                </div>

                <label for="sets" class="mt-1 text-md text-my-green">set</label>
                <div class="flex gap-2">
                    <input 
                    class="p-2  text-gray-500 focus:outline-my-cyan"
                    type="number"
                    required
                    v-model="sets"
                    id="sets">
                </div>
            </div>
        </form>    
                <button @click.prevent="createData" type="submit" class="bg-blue-light shadow-lg rounded-md text-deep-green w-24 border-deep-green hover:bg-white">Save</button>
        </div>       
            
    </div>
</template>

<script>
    import {computed, onUpdated, ref} from "vue"
    import {supabase} from './supabase.js'
    import {useRoute} from 'vue-router'
    export default {
    
    

        setup() {
            // const sets = ref('')
            // const weights = ref('')
            // const reps = ref('')
            // 
            
        }
    }
</script>