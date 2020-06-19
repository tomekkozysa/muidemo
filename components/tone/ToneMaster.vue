<template>
    <Group label="Tone Master Settings" :expanded="true">
        <mui-pad :sustain="300" :w="80" :h="80" :padding="0" mode="toggle" label="PLAY" @update="togglePlay">
            
        </mui-pad>
        <mui-spinner
            :rangeout="{min:1,max:320}"
            :start="84"
            :step = "1"
            :decimals = "0"
            @onchange="update($event,'bpm')"
            :label="'BPM'"
        />
        <mui-spinner
            :rangeout="{min:-60,max:1}"
            :start="-20"
            :step = "1"
            :decimals = "0"
            @onchange="update($event,'volume')"
            :label="'VOLUME'"
        />
        <mui-spinner
            
            :rangeout="{min:0,max:1}"
            :start="0"
            :step = ".1"
            :decimals = "1"
            @onchange="update($event,'swing')"
            :label="'SWING'"
        >
        <circle class="" cx="40" cy="52" r="30" stroke="cyan" stroke-width="1" fill="yellow" />
        </mui-spinner>

</Group>

</template>

<script>

import * as Tone from "tone";
import Group from '~/components/Group.vue';


export default {
    name: 'ToneMaster',
    components: {
        Group,
    },
    props:{
        bpm:Number,
        volume:Number,
    },
    data(){
        return{
            is_playing:false,
            // loop: null,
            // playbackRate  : 1 ,
            // iterations  : Infinity,
            // probability  : true ,
            // mute  : false,
            context_once:true,
            
        }
    },
    computed:{
       
    },
    mounted:function(){


        Tone.Transport.bpm.value = this.bpm;
        Tone.context.latencyHint = 'balanced'
        
        Tone.Transport.timeSignature = 4;
        Tone.Transport.loop = true;
        Tone.Transport.loopStart = 0;
        Tone.Transport.loopEnd = "2m";
        
    },
    methods:{
        onLoop:function(){
            console.log('loop!');
            
        },
        togglePlay:function(ev){

            if (Tone.context.state !== 'running' && this.context_once) {
                   Tone.context.resume();
                   this.context_once = false;
            }
            
            this.is_playing = ev.is_on;
            
            if(this.is_playing){
                // Tone.Transport.start("+0.1");
                Tone.Transport.start();
                // this.loop.start();
                // this.loop.start(0);
            }
            else{
                Tone.Transport.stop();
                // this.loop.stop();
                // this.loop.stop('+1n');
            }
        },

        update(ev,prop){

            if (prop === "bpm" )
            {
                Tone.Transport.bpm.value = ev;
            }
            else if (prop === "volume" )
            {
                Tone.Master.volume.value = ev;
            }
            else if (prop === "swing" )
            {
                Tone.Transport.swing = ev;
            }
            else{
                //  console.log('unknown prop', prop);
            }

        }
    }
}
</script>

