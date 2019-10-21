<template>
    <div class="contener_karty container text-center w-75 ">
      <div class="row">
      <div v-bind:class="{'effect-underline':circle1}" class="w-25 timer col-sm text-center "><animated-number class="num"  :value="overpopulation" :formatValue="formatToPrice" :duration="duration"/><br>  <font-awesome-icon icon="users" /></div>
      <div v-bind:class="{'effect-underline':circle2}" class="w-25 timer col-sm text-center "> <animated-number class="num" :value="climate" :formatValue="formatToPrice" :duration="duration"/> <br>  <font-awesome-icon style="font-size:1.1em" icon="leaf" /></div>
      <div v-bind:class="{'effect-underline':circle3}" class="w-25 timer col-sm text-center "><animated-number class="num"  :value="politics" :formatValue="formatToPrice" :duration="duration"/> <br>  <font-awesome-icon icon="handshake" /></div>
      <div v-bind:class="{'effect-underline':circle4}" class="w-25 timer col-sm text-center "><animated-number class="num"  :value="resources" :formatValue="formatToPrice" :duration="duration"/><br>  <font-awesome-icon icon="oil-can" /></div>
   
      </div>
    </div>
</template>

<script>
import AnimatedNumber from "animated-number-vue";
export default {
   components: {
    AnimatedNumber
  },
  name: "licznik",
  data() {
    return {
      value:15,
      duration: 200,
      overpopulation:15,
      climate:15,
      politics:15,
      resources:15,
      circle1:0,
      circle2:0,
      circle3:0,
      circle4:0
    };
  },
  methods: {
     formatToPrice(value) {
      return `${Number(value).toFixed(0)}`;
    },
    increase(val) {
      this.value = Number(this.value) + val;
    },
    decrease() {
      this.value = Number(this.value) - 500;
    },
    all(){
      let time =2;
    this.overpopulation-=time
    this.climate-=time
    this.politics-=time
    this.resources-=time
    }
  },
  mounted() {
   this.$root.$on('update',(overpopulation,climate,politics,resources)=>
   {
     this.increase(climate*5)
     this.increase(overpopulation*5)
     this.increase(politics*5)
     this.increase(resources*5)
  // this.all();
    this.politics+=politics*5
    this.climate+=climate*5
    this.overpopulation+=overpopulation*5
    this.resources+=resources*5
   
  

   if(this.overpopulation===0){
   this.$root.$emit("lose",0);
   }else if(this.climate===0){
   this.$root.$emit("lose",1);
   }else if(this.politics===0){
   this.$root.$emit("lose",2);
   }else if(this.resources===0) {
       this.$root.$emit("lose",3);
   }
     
    

   })
      this.$root.$on('circleLeave',()=>
   {
      this.circle1=0
      this.circle2=0
      this.circle3=0
      this.circle4=0
   })
   this.$root.$on('circle',(overpopulation,climate,politics,resources)=>
   {
     if(overpopulation!==0){
       this.circle1=1;
     }else{
       this.circle1=0
     }
     if(climate!==0){
       this.circle2=1;
     }else{
       this.circle2=0
     }
     if(politics!==0){
       this.circle3=1;
     }else{
       this.circle3=0
     }
     if(resources!==0){
       this.circle4=1;
     }else{
       this.circle4=0
     }
    
   })
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.timer:after {
  color: #fff;
	content: '';
  position: absolute;
  left: 0;
  display: inline-block;
  height: 1em;
  width: 100%;
  box-shadow: 0 5px 2px -2px white;
  margin-top: 10px;
  opacity: 0;
	-webkit-transition: opacity 0.35s, -webkit-transform 0.35s;
	transition: opacity 0.35s, transform 0.35s;
	-webkit-transform: scale(0,1);
	transform: scale(0,1);
}

.effect-underline:after {
  opacity: 1;
	-webkit-transform: scale(1);
	transform: scale(1);
}
.progress{
  padding:0;
  width:100px;
}
.contener_karty{
  margin:0 auto;
}
.timer {
  font-family: 'Source Code Pro', monospace;
    font-size:2em;
  font-weight: bold;
  padding: 0;
}
</style>
