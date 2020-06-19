<template>
    <div ref="drag">
</template>
<script>
import Logo from '~/components/Logo.vue'
import 'music-ui-vue'
import "music-ui-vue/mui.css";

// import muiTheme from 'music-ui-vue'

export default {
    props:{
        rangeout:Number,
    },
    data(){
        return{
            width:100,
            rangein:100,            
        }
    },
    methods:{
        mounted:function(){
            this.$refs.drag.addEventListener('mousedown',function(){})
        }
    }
}

</script>