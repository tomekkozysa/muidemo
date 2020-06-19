<template>
  <div class="container">

     <mui-spinner
                  :rangeout="{min:0,max:50}"
                  :start="10"
                  :step = "1"
                  :decimals = "1"
                  @onchange="e=>{}"
                  :label="'SPINNER'"
                  
            />

            
    <div class="mui-theme--default">
      <h1>
        mui: music user interface library
      </h1>

      <p>mui: is a user interface library designed for music and creative applications, written for vue.js </p>
      <p>Originally it's been created as an exercise in designing and developing a system for building user interfaces based around basic components. </p>
      <p>Please bare in mind, this is still an experimental phase and there is a lot of work and possible changes ahead. </p>


These include:
<ul>
<li>Spin </li>
<li>Trackpad </li>
<li>Slide</li>
<li>Pad</li>
</ul>
<h2>Installation</h2>
<code>
    npm i music-ui-vue 
</code>
or:
<code>
    yarn add music-ui-vue 
</code>

<h2>## Import mui:</h2>

<code>
    import  'music-ui-vue'
    import  "music-ui-vue/mui.css";
</code>

<h2>## Using mui:</h2>
<p>Each of the components can be customised via set of props. </p>
<ul>
<li><strong>throttle</strong> - defines the ratio in the speed of the interaction and output change</li>
<li><strong>rangeout</strong> - defines the component output range</li>
<li><strong>start</strong> - the default value</li>
<li><strong>step</strong> - the amount of growth</li>
<li><strong>decimals</strong> - defines the precision</li>
</ul>

<h2>
mui-spin</h2>
  
    <mui-spin :label="'SPIN DEMO'"     
    :throttle =".01"    
    :rangeout="{min:0,max:1}"    
    :start="0.01"    
    :step = ".001"    
    :decimals = "3"    
    />

    <code>
       <mui-spin :label="'SPIN DEMO'"     
    :throttle =".01"    
    :rangeout="{min:0,max:1}"    
    :start="0.01"    
    :step = ".001"    
    :decimals = "3"    
    />
    </code>
<h2>
mui-slide</h2>

	<mui-slide :label="'SLIDE'"  class="mui-slider-demo"    
    :throttle ="1"    
    :rangeout="{min:0,max:100}"    
    :start="50"    
    :step = "1"    
    :decimals = "0"    
    />

 <h2>mui-trackpad</h2>

    <mui-trackpad    
    :label="'TRCKPD DEMO '"    
    :rangeout="{x:{min:0,max:1},y:{min:0,max:1}}"    
    :start="{x:0,y:0}"    
    :throttle =".2"    
    :step = "{x:0.05,y:0.05}"    
    :decimals = "2"    
    />

<h2>mui-pad</h2>

    <mui-pad 
    :w="80" 
    :h="80" 
    :padding="0"  
    mode="toggle"  
    label="Pad"
    :index="0"
    />

<p>mui-pad due to specific type of interaction uses specific props, like mode, which can be defined as:</p>
<ul>
<li><strong>toggle</strong> – switch in between on & off states</li>
<li><strong>hold</strong> – remains active as long as the interaction continues </li>
<li><strong>shot</strong> – sends out a single hit, requires additional sustain prop to define the hit length in milliseconds</li>
</ul>

<h2>## Events:</h2>
<ul>
<li><strong>onchange</strong> – pad only, returns object with pad's index value, fires twice – at the start and the end of the interaction</li>
<li><strong>update </strong> – spin, slide and trackpad use this event to broadcast new value </li>
</ul>
<p>
Listening to the events:

   <code> @onchange="updateData"</code>
    
Event data can be a `Number`,  or an `Object`
</p>


<h2>## Design tokens</h2>

These are CSS variables, that allow you to customise visual properties of the components. You can overwrite them by assigning a CSS class to the components and re-defining the value of the variable:
<code>
    .demo{
    	--mui-background: rgba(192, 240, 16, 0.7);
    }
</code>
<h3>General/</h3>
<code>
    --mui-background:rgba(255,255,255,1);
    --bounding-rect-border-color:black;
    --bounding-rect-border-width:1; 
</code>

<h3>Label</h3>
<code>
    --mui-label-fill:rgba(0,0,0,0);
    --mui-label-text-color:white;    
    --mui-label-text-color:black;    
    --mui-label-font-size:10px;
</code>

<h3>Pad</h3>
<code>
    --mui-c-on:yellow;
    --mui-c-off:rgba(255,255,255,1);
    --mui-c-flash:yellow;
</code>
  
<h3>Spin</h3>
<code>
    --mui-spin-pointer-line-color:rgba(0,0,0,1);
    --mui-spin-pointer-line-width:1;
    --mui-spin-circle-color:rgba(0,0,0,1);
    --mui-spin-circle-fill:rgba(0,0,0,0);
    --mui-spin-circle-width:1;
</code>
  
  <h3>Slide</h3>
<code>
    --mui-slide-rect-fill:rgba(255,255,0,.8);
    --mui-slide-line-stroke:rgba(0,0,0,1);
    --mui-slide-line-stroke-width:1;
</code>

<h3>Trackpad</h3>
  <code>
    --mui-trpd-dot-fill:rgba(0,0,0,1);
    --mui-trpd-dot-stroke:none;
    --mui-trpd-dot-stroke-width:0;
    --mui-trpd-line-stroke:rgba(0,0,0,1);
    --mui-trpd-line-stroke-width:1;
  </code>
  





> Written with [StackEdit](https://stackedit.io/).







     
<!-- 
       <mui-spin  :label="'E. RELEASE'" class="mui-spin-demo"
        :throttle =".01"
        :rangeout="{min:0,max:1}"
        :start="0.01"
        :step = ".001"
        :decimals = "3"
        />

        <mui-slide  :label="'SLIDE'" class="mui-slider-demo"
        :throttle ="1"
        :rangeout="{min:0,max:100}"
        :start="50"
        :step = "1"
        :decimals = "0"
        />


         <mui-trackpad 
            :label="'dly:fdbck'"
            :rangeout="{x:{min:0,max:1},y:{min:0,max:1}}"
            :start="{x:.5,y:.5}"
            
            :throttle =".2"
            :step = "{x:0.05,y:0.05}"
            :decimals = "2"
    />
     <mui-pad :w="80" :h="80" :padding="0" mode="toggle" label="Pad" ></mui-pad>
 -->

        
        
        <h2>Components</h2>

        <p>Use [alt] or [shift] keys while dragging to modify sensitivity levels</p>

       

            <mui-spin :throttle=".1"
                  :rangeout="{min:0,max:50}"
                  :start="0"
                  :step = "1"
                  :decimals = "1"
                  @onchange="e=>{}"
                  :label="'SPIN'"
                  
            />
          
    

            <p> mui:slide by default moves along the Y or X axis. </p>


            <mui-slide

                    :label="'mui:slide'"
                    :rangeout="{min:0,max:100}"
                    :start="50"
                    @onchange="e=>{}"
                    :throttle="1"
                    :decimals="2"
                    :step="1"
            />
            <mui-slide
                    :vertical="true"
                    :label="'mui:slide'"
                    :rangeout="{min:0,max:100}"
                    :start="50"
                    @onchange="e=>{}"
                    :throttle="1"
                    :decimals="0"
                    :step="1"
            />

    
            <p> mui:trackpad allows simultanous interaction with two parameters </p>


            <mui-trackpad
                    :label="'X:Y'"
                    :rangeout="{x:{min:0,max:100},y:{min:0,max:100}}"
                    :start="{x:50,y:50}"
                    @onchange="e=>{}"
                    :step = "{x:.1,y:.1}"
                    :decimals = "2"
                    :throttle = "10"
            />

      
            <p> mui:pad will eiher send impulse or toggle on/off state  </p>


            <mui-pad :w="80" :h="80" :padding="0" mode="toggle" label="TOGGLE" />
            <mui-pad :w="80" :h="80" :padding="0" mode="hold" label="HOLD" />
            <mui-pad :sustain="1000" :w="80" :h="80" :padding="0" mode="shot" label="SINGLE 1s" />

            <!-- <p>mui Label</p>

            <svg width="80" height="20">
            <mui-label :x="2" :y="2" :w="76" :h="10" label="LABEL" class="label-demo" />
            </svg>
            
            <p>muiBoundbox</p>
            <svg width="80" height="80">
             <mui-boundbox :w="80" :h="80" class="boundbox-demo" />
            </svg>
            
            <p>muiGrid</p>
            <svg width="80" height="80">
                <mui-grid :w="80" :h="80" type="doublelabel" class="grid-demo" />
            </svg>
            <svg width="80" height="80">
                <mui-grid :w="80" :h="80" type="nolabel" class="grid-demo" />
            </svg>
            <svg width="80" height="80">
                <mui-grid :w="80" :h="80" type="singlelabel" class="grid-demo" />
            </svg> -->


            <h2> About </h2>
        <p> This library has started as my personal experiment mixing Vue.js and Tone.js, now the focus shifted towards creating a library or system if you like of small and customizable components.
            I established principles that would guide my thinking, introduce constraints and inform design, and here they are:</p>


        
        <ul>
            <li> design matters </li>
            <li> keep it simple</li>
            <li> make it configurable</li>
            <li> pick one size (80/80)</li>
            <li> entire component is interactive</li>

        </ul>
        <p> While working on the library, I also realised I will need to introduce the following, so far I only tapped on the first one.</p>
        <ul>
            <li> allow some level of theming and indiviudal component customisations ( feasbility unknown ) <sup>*</sup></li>
            <li> touch &amp; gestures support <sup>*</sup></li>
        </ul>


        <ul>Updates:

            <li>to fixed positon, handles decimals better + fixes</li>
            <li>theme management</li>
            
        </ul>






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
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=IBM+Plex+Mono&display=swap');

.mui-spin-demo{

  --mui-label-font-size:9px;
  --mui-label-fill:rgba(192, 240, 16, 0.7);

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
