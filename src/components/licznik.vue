<template>
    <div class="contener_karty container text-center w-75 ">
      <div class="row">
      <div class="w-25 timer col-sm text-center">{{przeludnienie}}  <font-awesome-icon icon="users" /><transition name="fade"> <i class="circle" v-if="circle1">	&bull;</i></transition></div>
      <div class="w-25 timer col-sm text-center">{{klimat}}  <font-awesome-icon style="font-size:1.1em" icon="leaf" /><transition name="fade"> <i class="circle" v-if="circle2">	&bull;</i></transition></div>
      <div class="w-25 timer col-sm text-center">{{polityka}}  <font-awesome-icon icon="handshake" /><transition name="fade"> <i class="circle" v-if="circle3">	&bull;</i></transition></div>
      <div class="w-25 timer col-sm text-center">{{zasoby}}  <font-awesome-icon icon="oil-can" /><transition name="fade"> <i class="circle" v-if="circle4">	&bull;</i></transition></div>
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
          if( this.przeludnienie==0 || this.klimat==0 || this.polityka==0 || this.zasoby==0){
       this.$root.$emit("lose");
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

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
