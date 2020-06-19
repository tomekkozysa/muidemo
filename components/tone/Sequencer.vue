<template>
   <Group>
        <mui-spin
                :label="'PROBABILITY'"
                :throttle=".1"
                :rangeout="{min:0,max:1}"
                :start="1"
                :step = ".1"
                :decimals = "1"
                @onchange="(e)=>tone.probability = e" 
                class="sequencer-probability" />

        <!-- <mui-spin
                :label="'PLY.BCK RATE'"
                :throttle=".1"
                :rangeout="{min:0,max:1}"
                :start="1"
                :step = ".01"
                :decimals = "2"
                @onchange="(e)=>tone.playbackRate = e" /> -->

        
        <mui-pad :w="80" :h="80" :padding="0" mode="toggle" label="HUMANIZE" @update="(e)=>tone.humanize = e.is_on"
        class="sequencer-humanize"></mui-pad>
        <mui-stepper :synth="tone" :w="80" :h="80" :cols="cols" :rows="rows" :index="headIndex" @patternUpdate="patternUpdate" @notestart="notestart" @noteend="noteend" 
        class="sequencer-stepper"/>
    </Group>
    
</template>

<script>

    
    import Tone from 'tone';
    import Group from '~/components/Group.vue';
    import GroupLabel from '~/components/GroupLabel.vue';

    export default {
    
    name: "Sequencer",  
    components:{
        Group,
        GroupLabel
            
    },
    props:{
        in:Tone.Instrument, // connect tone instrument the sequencer qill play along the pattern.
        duration: String,  // 
        length: Number,
        address:String, // mui store
       
    },
    data() {
        return {
            rows:4,
            cols:8,
            sequence:[],
            headIndex:-1,
            tone:new Tone.Sequence((time,n)=>{
               let t = Tone.TransportTime(time);
               console.log('sequence ', n)
            
                        if(n!= undefined && n !=""){
                            
                            this.in.triggerAttackRelease(n,this.duration,time,1);
                            
                        }
                
                },this.sequence, "16n"),

            
        };
    },
    computed:{},  
   
    methods: {  
        patternUpdate:function(pattern,lng){
            console.log('patternUpdate',pattern, pattern.length, lng);
            for(let i =0; i<pattern.length;i++){
                
                
                if(pattern[i] == ""){
                    // remove
                    this.sequence[i] = "";
                    this.tone.remove(i);
                    // console.log('removed at', i);
                }
                else{
                    // this[i] == n[i];
                    this.tone.at(i,pattern[i].note);
                    this.sequence[i] = pattern[i];
                    // console.log(`new note a ${i} value should be ${pattern[i].note} and is ${this.tone.at(i)}`,this.tone);
                }
            
            }

            console.log('patternUpdate -- sequence updated',this.sequence.length);
        },    
        initSequence:function(){
            
        }, 
        notestart:function(nO){
            console.log(nO,this.in);
             this.in.triggerAttack(nO.note,0,.5);
        },
        noteend:function(){
             this.in.triggerRelease();
        },
        sequenceStoreUpdate:function(){
             
        },
        //update, an method that emits an event like note played, or aything to do with the state things...
    }, // end of methods 
    mounted(){    
        // create a Tone sequence and play trigger the sound, 
        this.tone.start();
        // this.headloop.start();
        // this.tone.humanize = true;
        this.tone.probability = 1;
        this.tone.loop=true;
        this.tone.loopEnd = "2m"



        Tone.Transport.on("start",(e)=>{
            // console.log('TT on START',e)
        })
        Tone.Transport.on("stop",(e)=>{
            this.headIndex = -1;
        })


         Tone.Transport.scheduleRepeat((time)=>{

            let ta = Tone.Transport.position.split(':'); //t.toBarsBeatsSixteenths().split(':');

            let bar = ta[0];
            let beat = ta[1];
            let sth = Math.floor(ta[2]);

            let tt = bar * 16 + beat * 4 + sth;
            console.log('beat:::', tt,'[', bar, beat, sth,']')
            this.headIndex = tt;

	        

        }, "16n");





       



        console.log('sequencer mounted', this.tone,this.sequence,this.in);
    },
};

</script>
<style>
/* .lab{

    display:inline-block;
    cursor:pointer;
    user-select: none;
   
}


.mui-stepper-item{

    fill:white;
    stroke:black;    
}
.mui-stepper-item.is_selected{
    fill:yellow;
    stroke:black;    
}

.mui-stepper-item.is_recording{
    fill:red;
    stroke:black;    
} */


</style>
