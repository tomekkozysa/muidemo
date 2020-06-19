<template>
  <div class="container">
    
    <div class="mui-theme--default">
      <h1>
        mui: spin
      </h1>

               <div class="demo-rgb" :style="colors">
                 <svg width="80px" height="80">
                   <circle :cx="ddemo.dot.x" :cy="ddemo.dot.y" :r="ddemo.dot.r"  />
                 </svg>
                 </div>   
                    <mui-spin label="RED" class="demo-spin-red"    
                    :throttle =".1"    
                    :rangeout="{min:0,max:255}"    
                    :start="parseInt(ddemo.c.r)"    
                    :step = "1"    
                    :decimals = "0"    
                    @onchange="updater"
                    />
                    <mui-spin label="GREEN"  class="demo-spin-green"    
                    :throttle =".1"    
                    :rangeout="{min:0,max:255}"    
                    :start="parseInt(ddemo.c.g)"    
                    :step = "1"    
                    :decimals = "0"    
                    @onchange="updateg"
                    />
                    <mui-spin label="BLUE" class="demo-spin-blue"    
                    :throttle =".1"    
                    :rangeout="{min:0,max:255}"    
                    :start="parseInt(ddemo.c.b)"    
                    :step = "1"    
                    :decimals = "0"    
                    @onchange="updateb"
                    />     
                    <br />

                   


                    <mui-trackpad label="DOT POSITION"     
                    :throttle ="1"    
                    :rangeout="{x:{min:0,max:80},y:{min:0,max:80}}"    
                    :step="{x:1.0,y:1.0}"    
                    :start="{x:40.0,y:40}"    
                    :decimals = "0"    
                    @onchange="updateDot"
                    />     
  
                    <mui-slide :label="'DOT SIZE'" class="mui-slider-demo"    
                    :throttle ="1"    
                    :rangeout="{min:0,max:100}"    
                    :start="5"    
                    :step = "1"    
                    :decimals = "0"  
                    @onchange="(e)=>ddemo.dot.r = e"  
                    />
                 
    <p>
      <small>Use [alt] or [shift] keys while dragging to modify sensitivity levels</small>
    </p> 
  </div>
</div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import 'music-ui-vue'
import "music-ui-vue/mui.css";

// import muiTheme from 'music-ui-vue'

export default {
  components: {
    // Logo,
    // muiLabel
    // muiTheme
  },
  data(){
    
    return {
      ddemo:{
        throttle:0.001,
        c: { r: 120, g: 10, b: 100 },   
        dot:{x:40,y:40,r:5}
      },
      
    }
  },
  methods:{
    onUpdate:function(ev, prop){
      console.log('yay')
      this.ddemo[prop] = ev;
    },
    updater: function(v) {
      this.ddemo.c.r = v;
    },
    updateg: function(v) {
      this.ddemo.c.g = v;
    },
    updateb: function(v) {
      this.ddemo.c.b = v;
    },
    updateDot: function(v) {
      console.log(v);
      this.ddemo.dot.x = v.x;
      this.ddemo.dot.y = v.y;
    }
  },
    computed: {
    colors: function() {
      return "background:rgba(" + this.ddemo.c.r + "," + this.ddemo.c.g + "," + this.ddemo.c.b + ")"
    },

    colorshsla: function() {
      return "background:hsla(" + this.chsla.h + "," + this.chsla.s + "%," + this.chsla.l + "%," + this.chsla.a + ")"
      
    },   
  
    _throttle:function(){
      return this.ddemo.throttle;
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=IBM+Plex+Mono&display=swap');

.mui-spin-demo{

  --mui-label-font-size:9px;
  --mui-label-fill:rgba(192, 240, 16, 0.7);

}
.demo-rgb{
  width:80px;
  height:80px;
  margin:20px;
}

.demo-spin-blue{
  --mui-label-fill:rgba(0,0,255,0.6);
}
.demo-spin-green{
   --mui-label-fill:rgba(0,255,0,0.6);
}
.demo-spin-red{
  --mui-label-fill:rgba(255,0,0,0.6);
}    
.container {

  
  margin: 0 auto;
  min-height: 100vh;
  /* display: flex;
  justify-content: center;
  align-items: center;
  text-align: center; */
  font-family: 'IBM Plex Mono', monospace; 
  font-size:1em;
  

}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
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
