<template>
    <div class="container">
      <h1 class="title">Tone.js + mui:</h1>
      <p class="demoblob">
        This is a Tone.js basic sequencing demo. It's based on Tone.Sequence and Tone.AMSynth. User interface utilises my own library, mui:

      </p>

      <p class="demoblob">
      Here is how to use it:
      
      1. Tone Master controls, BPM, Volume, Swing:
      </p>
        <ToneMaster :bpm="40" :volume="-20" /> 
     
      <p class="demoblob"></p>


        
        <Group label="Sequencer">
            <sequencer v-if="amsynth" 
            class="sequencer"
            :in="amsynth" :duration="'32n'" :length="64" address="amsynth-sequencer" />
        </Group>

         <p class="demoblob">
      2. This is a Sequencer,
        Before you use it though, make sure the keyboard is "armed" first. Click the keyboard component, once highlighted it will listen to keyboard events.
      </p>
      <p class="demoblob">
        Back to Seqencer, pick a mode/action, start with Record. With that mode selected, you can pick when a note is played, with the armed keyboard you can pick a note.
      </p>



            <AMSynth ref="amsynth" />
        
    </div>
</template>

<script>
import ToneMaster from '~/components/tone/ToneMaster.vue';
import AMSynth from '~/components/tone/AMSynth.vue';
import Sequencer from '~/components/tone/Sequencer.vue';
import Group from '~/components/Group.vue';


import 'music-ui-vue'
import "music-ui-vue/mui.css";

// import muiTheme from 'music-ui-vue'

export default {
  components: {
    ToneMaster,
    AMSynth,
    Sequencer,
    Group
    
    // muiLabel
    // muiTheme
  },
  data(){
      return{
            amsynth:null,
            
      }
    
  },
  mounted:function(){
      // console.log('demo is mounted, ',this.$refs.amsynth.tone)
      this.amsynth = this.$refs.amsynth.tone;
  },
  methods:{},
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=IBM+Plex+Mono&display=swap');

.mui-spin-demo{


  --mui-label-fill:rgba(0, 0, 0, 0.1);

}
.container {

  margin: 0 auto;
  min-height: 100vh;
  font-family: 'IBM Plex Mono', monospace; 
  font-size:1em;
  
  --mui-label-fill:rgba(192, 240, 16, 0.1);
  --bounding-rect-border-width:1;

  --mui-label-font-size:9px;
  --mui-text-font-size:9px;

  --mui-spin-circle-color:rgba(12, 11, 11, 0.1);
  --mui-spin-circle-fill:rgba(0, 197, 187, 0.884);
  --mui-spin-circle-width:20;

}

.sequencer-probability{

  --mui-spin-circle-color:rgba(23, 39, 68, 1);
  --mui-spin-circle-fill:rgba(255, 220, 240, 1);
  --mui-spin-circle-width:5;

  --mui-spin-pointer-line-color:rgba(255, 220, 240, 1);
  --mui-spin-pointer-line-width:2;

}
.sequencer-probability:hover{

  --mui-spin-circle-width:20;
                
}


.demoblob{
  padding:20px;
  max-width: 500px;

}
.title {
  font-family: 'IBM Plex Mono', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 22px;
    padding:20px;
  color: #35495e;
  
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
