<template>
    <div>
        <div v-if="dataLoaded" class="mt-10 px-4">
            <div v-if="data.lenght ===0" class=" w-full flex-col items-center">
                <h1 class="text-2xl">No workout avalilable</h1>
                <router-link :to="{name: 'Generate'}"
                class="mt-6 py-2 px-6 rounded-sm text-sm
                text-white bg-deep-green duration-200 border-solid border-solid border-2 border-transparent hover:border-my-green hover:bg-white
                hover:text-deep-green">Generate Day</router-link>
            </div>

            <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
                <router-link
                class="flex-col items items-center bg-gret-400 p-8 shadow-md cursor-pointer"
                :to="{ name:'ViewWorkout', params: {workoutId:workout.id}}"
                v-for="(workout, index) in data"
                :key="index"
                >
                <img src="" alt="">
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Home",
    components:{}
}
</script>