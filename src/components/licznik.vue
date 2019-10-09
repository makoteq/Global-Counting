<template>
  <div class="hello">
    <div>
    <div class="timer text-center">przeludnienie {{przeludnienie}}</div>
    <div class="timer text-center">klimat {{klimat}}</div>
    <div class="timer text-center">polityka {{polityka}}</div>
    <div class="timer text-center">zasoby {{zasoby}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "licznik",
  data() {
    return {
      przeludnienie:2000,
      klimat:2000,
      polityka:2000,
      zasoby:2000

    };
  },
  methods: {
    
  },
  mounted() {
   this.$root.$on('update',(przeludnienie,klimat,polityka,zasoby)=>
   {
    this.polityka+=polityka*100
    this.klimat+=klimat*100
    this.przeludnienie+=przeludnienie*100
    this.zasoby+=zasoby*100
   })
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.timer{
  font-weight: bold;
}
</style>
