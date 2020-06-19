<template>
    <div class="group-label">
        <div class="group-label-text">{{label}}</div>
    </div>
        
</template>
<script>

// @ is an alias to /src

//import sequencerstep from '@/components/sequencerstep.vue'
// import muiLabel from '@/components/mui/base/muiLabel.vue'
export default {
    name: 'GroupLabel',
    props: {
        label:String,
        
    },
    mounted:function(){},
    
}
</script>

<style scoped>
   
    
    .group-label{

        --group-label-font-size : 12px;
        

        box-sizing: border-box;
        max-width:80px;
        height:80px;
        display:inline-block;
        padding:.25em;
        
        color:var(--group-label-text-color);
        background:var(--group-label-fill);
        
    }
    
    .group-label-text{
        writing-mode: tb;
        /* transform:scale(-1); */
        text-orientation: sideways;

        text-align:left;
        user-select: none;
        pointer-events: none;
        font-size:var(--group-label-font-size);
    }
</style>
