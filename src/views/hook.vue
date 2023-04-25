<template>
    <div>
        <h1 >try hook</h1>
        <button @click="onUpdated">update</button>
    </div>
</template>
<script>
    import {computed, onUpdated, beforeCreate, created, ref} from "vue"
export default {
    name: "hook",

    beforeCreate(){
        console.log("before create 1")
    },

    beforeMount(){
        console.log('before mount 2')
    },

    created() {
        console.log('created 3')
    },

    mounted() {
        console.log('mounted 4')
    },



    
}
</script>