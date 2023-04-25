<template>
    <div class="max-w-screen-md mx-auto px-4 py-10">
        <!-- <h1>{{data.workoutName}}</h1> -->
        <div class="p-8 flex gap-3 flex-col items-start bg-gray-100 rounded-md shadow-lg mb-4 " v-for="activity in data.activity"
          :key="activity.id">
                <button @click="deleteExcersise" >delete</button>
            <div class="grid grid-col-3 bg-gray-100 flex gap-5">
                <div>
                    <router-link :to="{name:'AddWorkout', params:{id:activity.id}}" class="justify-center text-my-green hover:text-my-cyan text-2xl">{{activity.excersiseDay}}</router-link>
                </div>
            </div>
        </div>
    </div> 
</template>

<script>
import {uid} from "uid"
import {ref, computed, onRenderTracked, onRenderTriggered} from "vue"
import {supabase} from "./supabase.js"
import {store} from "../store.js"
import {useRoute} from 'vue-router'

export default {
    data() {
        return{
            activity: []
        }
    },
    created() {
        this.getExcersises
    },
    myId(){
        return this.$route.params.id
    },
    name: "WorkoutDay",
    component: {},

    setup(mounted) {
        // const activity = ref(null)
        const errorMsg = ref(null)
        const statusMsg = ref(null)
        const data = ref({activity:[]})
        const dataLoaded = ref(null)
        const user = computed(() => store.state.user)
        const route = useRoute()
        // const excersiseId = route.params.activityId

        const addData = ()  => {
            excersises.value.push({
                set: "",
                reps: "",
                weight: ""
            }) 
            return
        }

        const getExcersises = async () => {
            try{
                const {data: activity,error} = await supabase
                .from('activityDay','activityExcersise')
                .select('*')
                if (error) throw error
                data.value = {activity:activity}
                dataLoaded.value = true

            }catch (error){
                errorMsg.value = error.message
                setTimeout(() =>{
                    errorMsg.value = false
                },5000)
            }
        }

        getExcersises()

        const deleteExcersise = async () => {
            console.log('function')
            try{
                const {data,error} = await supabase.form("activityDay").delete().eq('id','21')
                if (error) throw error
                statusMsg = 'Day scuessfully deleted'
            }catch (error){
                errorMsg.value = error.message
                setTimeout(() =>{
                    errorMsg.value = false
                },5000)
            }
        }

        
        return{addData,data,dataLoaded,deleteExcersise}
}
}
</script>