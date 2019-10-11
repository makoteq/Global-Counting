<template>
  <div>
    <div class="karta">
      <h3 style="font-weight:900!important;" class="font-weight-bold">{{tytul}}</h3>
      <img width="300px" :src="img" alt="photo" />
      <p class="font-weight-light">{{opis}}</p>
    </div>
    <button :disabled="!disable" @mouseleave="circleLeave()" @mouseover="over(1)" @click="submit(1)" class="btn-primary">  tak  </button>
    <button  :disabled="!disable" @mouseleave="circleLeave()" @mouseover="over(0)" @click="submit(0)" class="btn-primary">  nie </button>
  </div>
</template>

<script>
import karty from "../json_data/karty.json";
export default {
  name: "pole",
  data() {
    return {
      img: "",
      tytul: "",
      opis: "",
      przeludnienie: 0,
      klimat: 0,
      polityka: 0,
      zasoby: 0,
      kartyInfo: karty,
      count: 7,
      numbers: [0, 1, 2, 3, 4, 5, 6],
      i: 0,
      disable: 1
    };
  },
  methods: {
    //click
    submit(arg) {
        this.down(this.numbers[this.i+1], arg);
        this.send()
      console.log(this.numbers)
    },
    //download
    down(rand, arg) {
  
    
      if (arg == 1) {
        this.przeludnienie = this.kartyInfo[rand].tak.przeludnienie;
        this.klimat = this.kartyInfo[rand].tak.klimat;
        this.polityka = this.kartyInfo[rand].tak.polityka;
        this.zasoby = this.kartyInfo[rand].tak.zasoby;
      } else  {
        this.przeludnienie = this.kartyInfo[rand].nie.przeludnienie;
        this.klimat = this.kartyInfo[rand].nie.klimat;
        this.polityka = this.kartyInfo[rand].nie.polityka;
        this.zasoby = this.kartyInfo[rand].nie.zasoby;
      }
        if (this.i == this.count-1) {
        this.disable = 0;
      } else {
        this.i++;
      }
      this.img = this.kartyInfo[rand].img;
      this.tytul = this.kartyInfo[rand].tytul;
      this.opis = this.kartyInfo[rand].opis;
    
    },
    //wysyłanie danych zmian
    send(){
          this.$root.$emit(
        "update",
        this.przeludnienie,
        this.klimat,
        this.polityka,
        this.zasoby
      );
    },
    //wysyłanie circle
    circle(){
       this.$root.$emit(
        "circle",
          this.przeludnienie,
          this.klimat,
          this.polityka,
          this.zasoby
      );
    },
    circleLeave(){
      console.log('gggggggg')
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
    over(arg){
      console.log(this.i)
      let rand =this.numbers[this.i];
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
      this.circle();
    }
  },
  mounted() {
    //losowanko
     this.numbers = this.random(this.numbers);
     let rand =this.numbers[this.i];
  //  this.down(this.numbers[this.i]);
        this.img = this.kartyInfo[rand].img;
        this.tytul = this.kartyInfo[rand].tytul;
        this.opis = this.kartyInfo[rand].opis;
  }
};
</script>

<style lang="scss" scoped>
@import '../assets/colors.scss';
.karta {
  font-family: 'Source Code Pro', monospace;
  color:white;
  width: 30vw;
  background-color: $main;
  height: 40vh;
  margin: 0 auto;
}
</style>