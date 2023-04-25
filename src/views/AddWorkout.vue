<template>
    <div v-if='dataLoaded' class=" grid flex justify-items-center gap-5">

        <div>
            <div  class="text-2xl mb-7 font-simibold" v-for="activity in data.activity" :key="activity.id">
                <h1 class="text-gray-600 uppercase shadow-lg">
                   <h1 >{{activity.excersiseDay}} rerereere</h1>
                </h1>
            </div>
        </div>
        <h1 id="day">day</h1>
        <div class=' p-3 bg-gray-100 rounded-md shadow-lg'>
            <label for="excersise_name">Add Excersise Name</label>
            <form>
            <input
            class="p-1 mt-2 text-gray-500 focus:outline-my-cyan"
            type="text"
            required
            v-model="ExcersiseName"
            id="excersise_name">

            </form>
            <button @click="addName" class="bg-blue-light rounded-md text-deep-green w-24 border-deep-green mb-2 mt-4 hover:bg-white" type="submit">Add Name</button>
        </div>

        <div>
            <div v-for="excersiseName in data.excersiseName" :key="excersiseName.id">
                <h1>{{excersiseName.excersise_name}}</h1>
            </div>
        </div>
        <div>
            <div v-if="statusMsg || errorMsg" class="mb-5 p-5 bg-gray-100 rounded-md">
                <h1 class="text-gray-400">{{statusMsg}}</h1>
                <h1 class="text-red-400">{{errorMsg}}</h1>
            </div>
            
            <div></div>
            <div>
            </div>
            
        </div>
    </div>
</template>

<script>
    import {computed,onMounted,nextTick,ref} from "vue"
    import {supabase} from './supabase.js'
    import {useRoute} from 'vue-router'

 export default {
    name: 'AddWorkout',

    setup() {
        const ExcersiseName = ref('')
        const errorMsg = ref(null)
        const data = ref({workout:[]})
        const dataName = ref({workoutName:[]})
        const dataLoaded = ref(false)
        const myExcersise = ref('')
        const route = useRoute()
        const currentId = route.params.id
        const statusMsg = ref('')
           
        const createData = async () => {
            try {
                const {data,error} = await supabase.from ('activityExcersise').insert([
                    {
                        Set: sets.value,
                        Weights: weights.value,
                        Reps: reps.value,
                    }
                ])
                if (error) throw error 
                statusMsg.value= 'Data added scussesfully'
                sets.value = null
                weights.value = null
                reps.value = null
            }catch(error){
                errorMsg.value = `Error${error.message}`
                setTimeout (() =>{
                    errorMsg.value = false
                },5000)
            }
        }
        const addName = async () => {    
            console.log('try')

                try{
                    const {data,error} = await supabase.from("excersiseName").insert([
                        {
                            excersise_day:dayText,
                            excersise_name:ExcersiseName.value,
                        }
                    ])
                if (error) throw error
                ExcersiseName.value = null
                statusMsg.value = 'Name successfuly added'
                }
                catch(error){
                    errorMsg.value = `Error${error.message}`
                        data.value = {excersiseName:excersiseName}
                    setTimeout(() =>{
                        errorMsg.value = false
                    },5000)
                }
 
        // to fetch excersise day and update it to the DOM 
                }
        const getExcersises = async () => {
            try{
                const {data:activity,error} = await supabase.from ('activityDay').select("*").eq("id",currentId)
                dataLoaded.value = true
                data.value = {activity:activity}
                const day = data.value
                
            }
            catch (error){
                errorMsg.value = `Error${error.message}`
                setTimeout(() =>{
                    errorMsg.value = false
                },5000)
            }
        }

        const getExcersiseName = async () => {
            try{
                console.log('try2')
                    const {data: excersiseName,error} = await supabase.from ("excersiseName").select('*').eq("excersise_name",getDay)
                    dataLoaded.value = true
                    dataName.value = data.value

                    console.log('try3')
            }
            catch (error){
                errorMsg.value = `Error${error.message}`
                setTimeout (() =>{
                    errorMsg.value = false
                },5000)
            }
        }
        getExcersiseName()
        getExcersises()

        return{data,addName,createData,dataLoaded,myExcersise,statusMsg,ExcersiseName}
    },

}
</script>