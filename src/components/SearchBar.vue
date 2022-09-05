<template>
<div>
    <input type="text" :placeholder="placeholder" v-model.trim ="term" @keyup.enter="emitSearch">
    <button type="button" @click="emitSearch">{{buttonText}}</button>
</div>
</template>

<script>


export default {
    name: 'SearchBar',
    props: {
        placeholder:{
            type:String,
            required:false,
            default:'Cerca...'
        },
        buttonText:{
            type:String,
            required:false,
            default:'Cerca'
        },
    },
    data(){
        return{
            term:''
        }
    },
    methods:{
        emitSearch(){
            this.$emit('search',this.term)
        },
    }
}
</script>

<style>

</style>
