<template>
  <div>
    <div class="karta container w-75">
      <h3 style="font-weight:900!important;" class="font-weight-bold">{{tytul}}</h3>
      <img class="img-thumbnail" :src="img" alt="photo">
      <p class="font-weight-light">{{opis}}</p>
      <button v-if="end" :disabled="!disableSubmit" @click="submit()" class="btn-black btn-sm">NEXT</button>
    </div>
    <button
      v-if="end"
      :disabled="!disable"
      @mouseleave="circleLeave()"
      @mouseover="circle('tak')"
      @click="click(1)"
      class="btn-black btn-lg"
    >tak</button>
    <button
      v-if="end"
      :disabled="!disable"
      @mouseleave="circleLeave()"
      @mouseover="circle('nie')"
      @click="click(0)"
      class="btn-black btn-lg"
    >nie</button>
    <router-link v-if="!end" to="results">
      <button  class="btn-dark btn-lg">Go to results</button>
    </router-link>
    <p class="years fixed-bottom">{{years}} lata u władzy</p>
  </div>
</template>

<script>
import karty from "../json_data/karty.json";
import postacie from "../json_data/postacie.json";
export default {
  name: "pole",
  data() {
    return {
      img: "",
      tytul: "",
      opis: "",
      przeludnienie: 1,
      klimat: 1,
      polityka: 1,
      zasoby: 1,
      postacieInfo: postacie,
      kartyInfo: karty,
      count: 9,
      numbers: [],
      i: 0,
      disable: 1,
      disableSubmit: 0,
      years: 0,
      end: 1,
      wybor:0
    };
  },
  methods: {
    //next
    submit() {
      
      this.disableSubmit = 0;
      this.years++;
      this.disable = 1;
      this.circleLeave();
      this.down(this.wybor);
      this.send();
          if (this.i === this.count - 1) {
        this.disable = 0;
      } else {
        this.i = this.i + 1;
      }
      this.img = this.kartyInfo[this.numbers[this.i]].img;
      this.tytul = this.kartyInfo[this.numbers[this.i]].tytul;
      this.opis = this.kartyInfo[this.numbers[this.i]].opis;
      console.log(this.i + "mountede");

 
    },
    //click
    click(arg) {
      this.wybor = arg;
      this.disableSubmit = 1;
      this.disable = 0;
      console.log()
    },
    //download
    down( arg) {
       let rand = this.numbers[this.i];
       console.log(this.i)
       if (arg == 1) {
        this.przeludnienie = this.kartyInfo[rand].tak.przeludnienie;
        this.klimat = this.kartyInfo[rand].tak.klimat;
        this.polityka = this.kartyInfo[rand].tak.polityka;
        this.zasoby = this.kartyInfo[rand].tak.zasoby;
      } else {
        this.przeludnienie = this.kartyInfo[rand].nie.przeludnienie;
        this.klimat = this.kartyInfo[rand].nie.klimat;
        this.polityka = this.kartyInfo[rand].nie.polityka;
        this.zasoby = this.kartyInfo[rand].nie.zasoby;
      }
    },
    //wysyłanie danych zmian
    send() {
      console.log(this.i)
      console.log('send'+  this.przeludnienie+','
      +this.klimat+','+
       + this.polityka+','+
       + this.zasoby)
      this.$root.$emit(
        "update",
        this.przeludnienie,
        this.klimat,
        this.polityka,
        this.zasoby
      );
    },
    //wysyłanie circle
    circle(arg) {
        let rand = this.numbers[this.i];
           if (arg === 1) {
          this.$root.$emit(
        "circle",
        this.kartyInfo[rand].tak.przeludnienie,
        this.kartyInfo[rand].tak.klimat,
        this.kartyInfo[rand].tak.polityka,
        this.kartyInfo[rand].tak.zasoby,
      );
      } else {
          this.$root.$emit(
        "circle",
        this.kartyInfo[rand].nie.przeludnienie,
        this.kartyInfo[rand].nie.klimat,
       this.kartyInfo[rand].nie.polityka,
        this.kartyInfo[rand].nie.zasoby,
      );
      }
  
    },
    circleLeave() {
      this.$root.$emit("circleLeave");
    },
    //losowamnie
    random(a) {
      //mieszanko tablic
      let j, x, i;
      for (i = a.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        x = a[i];
        a[i] = a[j];
        a[j] = x;
      }
      return a;
    },
  },
  mounted() {
    //generate array
    for (let i = 0; i < this.count + 1; i++) {
      this.numbers.push(i);
      console.log(i);
    }

    this.$root.$on("lose", arg => {
      this.end = 0;
      console.log("lose" + arg);
      this.disable = 0;
      this.disableSubmit = 0;
      this.tytul = this.postacieInfo[arg].tytul;
      this.opis = this.postacieInfo[arg].opis;
      // this.opis=this.postacie.arg;
      //   this.$router.push({name:'results'})
    });
    //losowanko
    this.numbers = this.random(this.numbers);
    console.log(this.numbers);
    console.log(this.i + "mountede");
    let rand = this.numbers[this.i];
    //  this.down(this.numbers[this.i]);
    this.img = this.kartyInfo[rand].img;
    this.tytul = this.kartyInfo[rand].tytul;
    this.opis = this.kartyInfo[rand].opis;
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/colors.scss";
.karta {
  padding: 0;
  font-family: "Source Code Pro", monospace;
  color: white;
  background-color: $main;
}
</style>