<template>
    <div class="contener_karty container text-center w-75 ">
      <div class="row">
      <div v-bind:class="{'effect-underline':circle1}" class="w-25 timer col-sm text-center ">{{przeludnienie}}  <font-awesome-icon icon="users" /></div>
      <div v-bind:class="{'effect-underline':circle2}" class="w-25 timer col-sm text-center ">{{klimat}}  <font-awesome-icon style="font-size:1.1em" icon="leaf" /></div>
      <div v-bind:class="{'effect-underline':circle3}" class="w-25 timer col-sm text-center ">{{polityka}}  <font-awesome-icon icon="handshake" /></div>
      <div v-bind:class="{'effect-underline':circle4}" class="w-25 timer col-sm text-center ">{{zasoby}}  <font-awesome-icon icon="oil-can" /></div>
      </div>
    </div>
</template>

<script>
export default {
  name: "licznik",
  data() {
    return {
      przeludnienie:15,
      klimat:15,
      polityka:15,
      zasoby:15,
      circle1:0,
      circle2:0,
      circle3:0,
      circle4:0
    };
  },
  methods: {
    all(){
      let time =2;
    this.polityka-=time
    this.klimat-=time
    this.przeludnienie-=time
    this.zasoby-=time
    }
  },
  mounted() {
   this.$root.$on('update',(przeludnienie,klimat,polityka,zasoby)=>
   {
  // this.all();
    this.polityka+=polityka*5
    this.klimat+=klimat*5
    this.przeludnienie+=przeludnienie*5
    this.zasoby+=zasoby*5
   
   if(this.przeludnienie==0){
   this.$root.$emit("lose",0);
   }else if(this.klimat==0){
   this.$root.$emit("lose",1);
   }else if(this.polityka==0){
   this.$root.$emit("lose",2);
   }else if(this.zasoby==0) {
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
   this.$root.$on('circle',(przeludnienie,klimat,polityka,zasoby)=>
   {
     if(przeludnienie!=0){
       this.circle1=1;
     }else{
       this.circle1=0
     }
     if(klimat!=0){
       this.circle2=1;
     }else{
       this.circle2=0
     }
     if(polityka!=0){
       this.circle3=1;
     }else{
       this.circle3=0
     }
     if(zasoby!=0){
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
