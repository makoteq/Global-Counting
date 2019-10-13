<template>
  <div>
    <div class="karta container w-75">
      <h3 style="font-weight:900!important;" class="font-weight-bold">{{tytul}}</h3>
      <img class="img-thumbnail" :src="img" alt="photo" />
      <p class="font-weight-light">{{opis}}</p>
      <button v-if="end" :disabled="!disableSubmit" @click="submit()" class="btn-primary btn-sm">NEXT</button>
    </div>
    <button
      v-if="end"
      :disabled="!disable"
      @mouseleave="circleLeave()"
      @mouseover="over(1)"
      @click="click(1)"
      class="btn-primary btn-lg"
    >tak</button>
    <button
    v-if="end"
      :disabled="!disable"
      @mouseleave="circleLeave()"
      @mouseover="over(0)"
      @click="click(0)"
      class="btn-primary btn-lg"
    >nie</button>
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
      postacieInfo:postacie,
      kartyInfo: karty,
      count: 9,
      numbers: [],
      i: 0,
      disable: 1,
      disableSubmit: 0,
      years: 0,
      end:1
    };
  },
  methods: {
    //next
    submit() {
      this.disableSubmit = 0;
      this.years++;
      this.disable = 1;
      this.circleLeave();
      if (this.i == this.count - 1) {
        this.disable = 0;
      } else {
        this.i = this.i + 1;
      }
      console.log(this.i + "mountede");

      this.down(this.numbers[this.i]);
    },
    //click
    click(arg) {
      this.disableSubmit = 1;
      this.disable = 0;

      this.send();
      console.log(this.numbers);
    },
    //download
    down(rand, arg) {
      this.img = this.kartyInfo[rand].img;
      this.tytul = this.kartyInfo[rand].tytul;
      this.opis = this.kartyInfo[rand].opis;
      /* if (arg == 1) {
        this.przeludnienie = this.kartyInfo[rand].tak.przeludnienie;
        this.klimat = this.kartyInfo[rand].tak.klimat;
        this.polityka = this.kartyInfo[rand].tak.polityka;
        this.zasoby = this.kartyInfo[rand].tak.zasoby;
      } else {
        this.przeludnienie = this.kartyInfo[rand].nie.przeludnienie;
        this.klimat = this.kartyInfo[rand].nie.klimat;
        this.polityka = this.kartyInfo[rand].nie.polityka;
        this.zasoby = this.kartyInfo[rand].nie.zasoby;
      }*/
    },
    //wysyłanie danych zmian
    send() {
      this.$root.$emit(
        "update",
        this.przeludnienie,
        this.klimat,
        this.polityka,
        this.zasoby
      );
    },
    //wysyłanie circle
    circle() {
      this.$root.$emit(
        "circle",
        this.przeludnienie,
        this.klimat,
        this.polityka,
        this.zasoby
      );
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
    over(arg) {
      console.log(this.i);
      let rand = this.numbers[this.i];
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
    //generate array
    for (let i = 0; i < this.count + 1; i++) {
      this.numbers.push(i);
      console.log(i);
    }

    this.$root.$on("lose", arg => {
      this.end=0;
      console.log("lose"+arg);
      this.disable = 0;
      this.disableSubmit = 0;
      switch (arg) {
        case 0:
          this.tytul='Głód';
          this.opis=this.postacieInfo[0].glod;
          break;
        case 1:
          this.tytul='Śmierć';
          this.opis=this.postacieInfo[0].smierc;
          break;
        case 2:
          this.tytul='Wojna';
          this.opis=this.postacieInfo[0].wojna;
          break;
        case 3:
          this.tytul='Wojna'
          this.opis=this.postacieInfo[0].wojna;
          break;
      }
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