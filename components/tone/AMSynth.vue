<template>
    <div v-if="tone">
        <Group label="AM Synth"> 
        
            <mui-spinner :label="'VOLUME'"
                :rangeout="{min:-60,max:10}"
                :start="settings.volume"
                :step = ".1"
                :decimals = "1"
                @onchange="(e)=>this.tone.volume.value = e" />

            <mui-spinner :label="'HARMONICITY'"
                :rangeout="{min:0,max:4}"
                :start="settings.harmonicity"
                :step = ".01"
                :decimals = "2"
                @onchange="(e)=>this.tone.harmonicity.value = e" />

        
            <mui-spinner :label="'DETUNE'" 
                :rangeout="{min:-2000,max:2000}"
                :start="settings.detune"
                :step = ".5"
                :decimals = "1"        
                @onchange="(e)=>this.tone.detune.value = e" />           
        

            <GroupLabel label="envelope" /> 
            
            <mui-slider :w="40" :label="'ATCK'"
                
                :start="settings.envelope.attack"
                :rangeout="{min:0.001,max:2}"
                :step = ".001"
                :decimals = "3"
                @onchange="(e)=>this.tone.envelope.attack = e" 
                class="envelope-slider" />

            <mui-slider :w="40" :label="'DCAY'" 
                
                :rangeout="{min:0,max:4}"
                :start="settings.envelope.decay"
                :step = ".01"
                :decimals = "2"
                @onchange="(e)=>this.tone.envelope.decay = e" 
                class="envelope-slider" />

            <mui-slider :w="40" :label="'SUSTN'"
                
                :start="settings.envelope.sustain"
                :rangeout="{min:0.001,max:2}"
                :step = ".001"
                :decimals = "3"
                @onchange="(e)=>this.tone.envelope.sustain = e" 
                class="envelope-slider" />
            
            <mui-slider :w="40"  :label="'RLSE'"
                
                :rangeout="{min:0.01,max:2}"
                :start="settings.envelope.release"
                :step = ".01"
                :decimals = "2"
                @onchange="(e)=>this.tone.envelope.release = e" 
                class="envelope-slider" />


            <GroupLabel label="mod_envelope" />              
            
            <mui-slider :w="40" :label="'ATCK'"
                
                :start="settings.modulationEnvelope.attack"
                :rangeout="{min:0.001,max:2}"
                :step = ".001"
                :decimals = "3"
                @onchange="(e)=>this.tone.modulationEnvelope.attack = e" />

            <mui-slider :w="40" :label="'DCAY'" 
                
                :rangeout="{min:0,max:4}"
                :start="settings.modulationEnvelope.decay"
                :step = ".01"
                :decimals = "2"
                @onchange="(e)=>this.tone.modulationEnvelope.decay = e" />

            <mui-slider :w="40" :label="'SUSTN'"
                
                :start="settings.modulationEnvelope.sustain"
                :rangeout="{min:0.001,max:2}"
                :step = ".001"
                :decimals = "3"
                @onchange="(e)=>this.tone.modulationEnvelope.sustain = e" />
            
            <mui-slider :w="40"  :label="'RLSE'"
                
                :rangeout="{min:0.01,max:2}"
                :start="settings.modulationEnvelope.release"
                :step = ".01"
                :decimals = "2"
                @onchange="(e)=>this.tone.modulationEnvelope.release = e" />

            <GroupLabel label="oscilators" />  

            <mui-listpick label="OSC. TYPE" :list="['amsine2','sine','triangle','sawtooth','square','fatsine','fattriangle','fatsawtooth','fatsquare']" :pick="1" @update="(e)=>{this.tone.oscillator.type = e}" />
            <mui-listpick label="MOD. TYPE" :list="['amsine2','sine','triangle','sawtooth','square','fatsine','fattriangle','fatsawtooth','fatsquare']" :pick="1" @update="(e)=>{this.tone.modulation.type = e}" /> 

        </Group>
    </div>
</template>
<script>




import Tone from "tone";
import Group from '~/components/Group.vue';
import GroupLabel from '~/components/GroupLabel.vue';

export default {
    name: 'AMSynth',
    components: {

        Group,
        GroupLabel,
        
    },
    props:{
        uid:String,
    },
    data(){
        return{
            // tone:null,
            frequency:100,
            detune:0,
            spread:0,
            count:10,
            on:false,
            fmOsc:null,
            iskey:false,
            key:[],

            settings:{
                volume:0,
                duration:'32n',
                harmonicity  : 0,
                detune  : 0,
                oscillator  : {
                    type  : 'sine',
                    modulationType : "sine",
                    harmonicity: 1.01
                } ,
                envelope  : {
                    attack  : .001,
                    decay  : 0.01,
                    sustain  : 1,
                    release  : 0.5
                },
                modulation  : {
                   type  : 'sine'
                } ,
                modulationEnvelope  : {
                    attack  : 0.001,
                    decay  : 0.5,
                    sustain  : 1,
                    release  : 0.5
                }
            },
            settings2:{
                 volume:0,
                duration:'32n',
                detune  : 0,
                "harmonicity": 2,
                "oscillator": {
                    "type": "amsine2",
                    "modulationType" : "sine",
                        "harmonicity": 1.01
                },
                "envelope": {
                    "attack": 0.006,
                    "decay": 4,
                    "sustain": 0.04,
                    "release": 1.2
                },
                "modulation" : {
                    "volume" : 13,
                    "type": "amsine2",
                    "modulationType" : "sine",
                        "harmonicity": 12
                },
                "modulationEnvelope" : {
                    "attack": 0.006,
                    "decay": 0.2,
                    "sustain": 0.2,
                    "release": 0.4
                }
            },
            tone:null,
            // tone:new Tone.AMSynth(this.settings),
            pattern:[],//out from the stepper and into the store,
            sequence:[]//out of the store and into sequencer,

           
            
        }
    },
    computed:{
        json_settings:function(){
            return JSON.stringify(this.settings, null, 2)
        }
    },
    created(){
    
      

    
    },
    mounted:function(){


          this.tone = new Tone.AMSynth(this.settings);
                this.tone.toMaster();
        
        // this.tone = new Tone.FMSynth(this.settings);
        console.log('hello AMSynth', this.tone);
        // this.tone.chain(this.$refs.compressor.tone,  this.$refs.wahwah.tone,this.$refs.ppd.tone,this.$refs.freeverb.tone);


    },

}
</script>

<style scoped>
.lab{
    overflow:visible;
   
      
}
.envelope-slider{

      --mui-label-font-size:9px;
}
</style>