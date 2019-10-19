<template>
  <div>
    <div class="karta container w-75">
      <h3 style="font-weight:900!important;" class="font-weight-bold">{{title}}</h3>
      <img class="img-thumbnail" :src="img" alt="photo">
      <p class="font-weight-light">{{des}}</p>
      <button v-if="end" :disabled="!disableSubmit" @click="submit()" class="btn-black btn-sm">NEXT</button>
    </div>
    <button
      v-if="end"
      :disabled="!disable"
      @mouseleave="circleLeave()"
      @mouseover="circle('yes')"
      @click="click(1)"
      class="btn-black btn-lg"
    >Tak</button>
    <button
      v-if="end"
      :disabled="!disable"
      @mouseleave="circleLeave()"
      @mouseover="circle('no')"
      @click="click(0)"
      class="btn-black btn-lg"
    >Nie</button>
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
      title: "",
      des: "",
      overpopulation: 1,
      climate: 1,
      politics: 1,
      resources: 1,
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
      this.title = this.kartyInfo[this.numbers[this.i]].title;
      this.des = this.kartyInfo[this.numbers[this.i]].des;
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
        this.overpopulation = this.kartyInfo[rand].yes.overpopulation;
        this.climate = this.kartyInfo[rand].yes.climate;
        this.politics = this.kartyInfo[rand].yes.politics;
        this.resources = this.kartyInfo[rand].yes.resources;
      } else {
        this.overpopulation = this.kartyInfo[rand].no.overpopulation;
        this.climate = this.kartyInfo[rand].no.climate;
        this.politics = this.kartyInfo[rand].no.politics;
        this.resources = this.kartyInfo[rand].no.resources;
      }
    },
    //wysyłano danych zmian
    send() {
      console.log(this.i)
      console.log('send'+  this.overpopulation+','
      +this.climate+','+
       + this.politics+','+
       + this.resources)
      this.$root.$emit(
        "update",
        this.overpopulation,
        this.climate,
        this.politics,
        this.resources
      );
    },
    //wysyłano circle
    circle(arg) {
        let rand = this.numbers[this.i];
           if (arg === 1) {
          this.$root.$emit(
        "circle",
        this.kartyInfo[rand].yes.overpopulation,
        this.kartyInfo[rand].yes.climate,
        this.kartyInfo[rand].yes.politics,
        this.kartyInfo[rand].yes.resources,
      );
      } else {
          this.$root.$emit(
        "circle",
        this.kartyInfo[rand].no.overpopulation,
        this.kartyInfo[rand].no.climate,
       this.kartyInfo[rand].no.politics,
        this.kartyInfo[rand].no.resources,
      );
      }
  
    },
    circleLeave() {
      this.$root.$emit("circleLeave");
    },
    //losowamno
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
      this.title = this.postacieInfo[arg].title;
      this.des = this.postacieInfo[arg].des;
      // this.des=this.postacie.arg;
      //   this.$router.push({name:'results'})
    });
    //losowanko
    this.numbers = this.random(this.numbers);
    console.log(this.numbers);
    console.log(this.i + "mountede");
    let rand = this.numbers[this.i];
    //  this.down(this.numbers[this.i]);
    this.img = this.kartyInfo[rand].img;
    this.title = this.kartyInfo[rand].title;
    this.des = this.kartyInfo[rand].des;
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