<template>
  <div>
    <div class="karta">
      <h3 class="font-weight-bold">{{tytul}}</h3>
      <p class="font-weight-light">{{opis}}</p>
    </div>
    <button @click="tak" class="btn-primary">tak</button>
    <button @click="nie" class="btn-primary">nie</button>
  </div>
</template>

<script>
import karty from "../json_data/karty.json";
export default {
  name: "pole",
  data() {
    return {
      tytul: "test",
      opis: "test opisu",
      przeludnienie: 0,
      klimat: 0,
      polityka: 0,
      zasoby: 0,
      kartyInfo: karty
    };
  },
  methods: {
    tak() {
      this.$root.$emit(
        "update",
        this.przeludnienie,
        this.klimat,
        this.polityka,
        this.zasoby
      );
    },
    nie() {}
  },
  mounted() {
    //losowanko
    this.tytul = this.kartyInfo[0].tytul;
    this.opis = this.kartyInfo[0].opis;
    this.przeludnienie = this.kartyInfo[0].tak.przeludnienie;
    this.klimat = this.kartyInfo[0].tak.klimat;
    this.polityka = this.kartyInfo[0].tak.polityka;
    this.zasoby = this.kartyInfo[0].tak.zasoby;
  }
};
</script>

<style lang="scss" scoped>
.karta {
  width: 30vw;
  background-color: grey;
  height: 40vh;
  margin: 0 auto;
}
</style>