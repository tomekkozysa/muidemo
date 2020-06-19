<template>
<div class="group" >
    <GroupLabel :label="label" @click="toggle"/>
        <div class="group-content" :class="{is_expanded:is_expanded}">
        <slot>
        </slot>
    </div>
</div>
</template>
<script>

// @ is an alias to /src

import GroupLabel from '@/components/GroupLabel.vue'
export default {
    name: 'Group',
    props: {
        label:String,
        expanded:Boolean,
    },
    components: {
        // 'mui-label':muiLabel,
        GroupLabel,
    },
    data(){
        return {
            is_expanded:true,//this.expanded,
        }
    },
    mounted:function(){},
    methods:{
        toggle:function(){
            this.is_expanded = !this.is_expanded;
        }
    },
}
</script>

<style scoped>
    .group{
        /* padding:1em 0; */
        /* border:1px dashed black; */
        /* display:inline-block; */
        /* -webkit-box-reflect: below 0px -webkit-gradient(linear, left top, left bottom, from(transparent), to(rgba(250, 250, 250, 0.2))); */

         display: flex;
        flex-direction: row;
    }
    .group:hover{
        z-index:10000;
        position: relative;
    }
    .group-content{
        /* display:inline-block; */
        display:none;
        

        
    }
    .group-content.is_expanded{
        /* display:inline-block; */
display: flex;
       
       
    }
   
    
</style>
