<template>
    <div class="container">
      <h1 class="title">Tone.js + mui:</h1>
      <p class="demoblob">

        Hi, this is a sequencing demo using Tone.js and mui: created for Bob@Charanga. 
        It's uses Tone.Sequence and Tone.AMSynth. User interface utilises my own library, mui:.



      </p>

      <p class="demoblob" v-if="showhints">
     
      Here is a quick guide on how to use it:
      Below are Tone Master controls, BPM, Volume, Swing:
      </p>
        <ToneMaster :bpm="40" :volume="-20" /> 
     
      <p class="demoblob" v-if="showhints"></p>        
      <Group label="Sequencer">
          <sequencer v-if="amsynth" 
          class="sequencer"
          :in="amsynth" :duration="'32n'" :length="64" address="amsynth-sequencer" />
      </Group>
      <p class="demoblob" v-if="showhints">
      2. This is a Sequencer, is a little bit quirky.  It starts playing as soon as you hit the PLAY button in Tone Master control.
      </p>
      <p class="demoblob" v-if="showhints">
        Before you use it, make sure the keyboard is "armed". Click the keyboard component, once highlighted it will listen to the actual keyboard events - the A,W,S,D etc... will have notes assigned now.
        <strong> Use Z / X to change the octave. </strong> 
      </p>
      <p class="demoblob" v-if="showhints">
        
      Back to Sequencer, the way to use it, is through the MODE panel:<br />

      1. Select "Record" mode. <br />
      2. Select a cell or cells in the grid, to determine when the note is played. <br />
      3. With keyboard component armed, use your actual keyboard to schedule a particular note.<br />
      4. Other modes can misbehave, try the "random" one, it will quickly select a bunch of random cells in the sequencer. Switch back to record and you can schedule multiple random notes!

    
      </p>



      <AMSynth ref="amsynth" />

 
   

      <p class="demoblob" v-if="showhints">
        <strong> When interacting with the UI, you can use ALT or SHIFT key to affect sensitivity of a dial.</strong>
      </p>
      <p class="demoblob" v-if="showhints">
A little bit more about mui: – music interface library. SVG based, uses CSS vars as design tokens. Some components use vue slots to inject a bespoke SVG element like an extra circle in the SWING dial. 
      </p>
      <p class="demoblob" v-if="showhints">
  Currently mui: under construction and kept as a private repo, the code for this demo can be found here:

<a href="https://github.com/tomekkozysa/muidemo" > https://github.com/tomekkozysa/muidemo </a>

      </p>
      <p class="demoblob">

             <mui-pad label="TOGGLE HINTS" mode="toggle" :w="80" :h="20" :padding="0"
      @update="(e)=>{this.showhints = !this.showhints }"/>

      </p>

        
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
            showhints: true,
            
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
