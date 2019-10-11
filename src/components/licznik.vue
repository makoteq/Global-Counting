<template>
  <div class="hello">
    <div class="contener_karty container text-center ">
      <!-- 
      <div class="row">
<div class="progress col-sm ">
  <div id="dynamic" class="progress-bar progress-bar-success progress-bar-striped active" role="progressbar" aria-valuenow="10" aria-valuemin="0" aria-valuemax="20" :style="{width: przeludnienie+'%'}">
    <span id="current-progress"></span>
  </div>
</div>
<div class="progress col-sm ">
  <div id="dynamic" class="progress-bar progress-bar-success progress-bar-striped active" role="progressbar" aria-valuenow="10" aria-valuemin="0" aria-valuemax="20" :style="{width: klimat+'%'}">
    <span id="current-progress"></span>
  </div>
</div>
<div class="progress  col-sm ">
  <div id="dynamic" class="progress-bar progress-bar-success progress-bar-striped active" role="progressbar" aria-valuenow="10" aria-valuemin="0" aria-valuemax="20" :style="{width: polityka+'%'}">
    <span id="current-progress"></span>
  </div>
</div>
<div class="progress col-sm ">
  <div id="dynamic" class="progress-bar progress-bar-success progress-bar-striped active" role="progressbar" aria-valuenow="10" aria-valuemin="0" aria-valuemax="20" :style="{width: zasoby+'%'}">
    <span id="current-progress"></span>
  </div>
</div>
</div>
 -->
      <div class="row">
      <div class="timer col-sm text-center">{{przeludnienie}}<i v-if="circle1">	&bull;</i></div>
      <div class="timer col-sm text-center">{{klimat}}<i v-if="circle2">	&bull;</i></div>
      <div class="timer col-sm text-center">{{polityka}}<i v-if="circle3">	&bull;</i></div>
      <div class="timer col-sm text-center">{{zasoby}}<i v-if="circle4">	&bull;</i></div>
      </div>
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
    console.log('up')
    this.polityka+=polityka*5
    this.klimat+=klimat*5
    this.przeludnienie+=przeludnienie*5
    this.zasoby+=zasoby*5
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
  width:500px;
  height:100px;
  margin:0 auto;
}
.timer {
  font-size:2em;
  font-weight: bold;
}
</style>
