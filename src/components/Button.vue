<template>
    <button @click="onClick()" :style="{background:color}">{{text}}</button>
</template>

<script>
export default {
    name: "Button",
    props: {
     color: String,
     text: String
    },
    methods:{
        onClick(){
            this.$emit('btn-click');
        }
    }

}
</script>
<style>
</style>