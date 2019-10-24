<template>
  <div>
    <div class="karta container w-75">
      <h3 style="font-weight:900!important;" class="text-success font-weight-bold ">{{title}}</h3>
      <img class="img-thumbnail" style="min-width:30vw; max-width:60vw" :src="img" alt="photo">
      <p class=" font-weight-light">{{des}}</p>
    </div>
    <button
      v-if="end"
      @mouseleave="circleLeave()"
      @mouseover="circle(1)"
      @click="click(1)"
      class="btn-black btn-lg"
    >Tak</button>
    <button
      v-if="end"
      @mouseleave="circleLeave()"
      @mouseover="circle(0)"
      @click="click(0)"
      class="btn-black btn-lg"
    >Nie</button>
    <router-link v-if="!end" :to="{ name: 'results', params: {years: this.years,why:this.why } }">
      <button  class="btn-dark btn-lg">Wyniki</button>
    </router-link>
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
      years: 0,
      end: 1,
      wybor:0,
      why:0
    };
  },
  methods: {
    //next

    //click
    click(arg) {
      this.years++;
      this.circleLeave();
      this.down(this.wybor);
      this.send();
        if (this.i === this.count - 1) {
          this.why=4;
        this.des = this.postacieInfo[0].des;
        this.title = this.postacieInfo[0].title;
        this.img = this.postacieInfo[0].img;
        this.end=0;
      } else {
      this.i = this.i + 1;
      }
      if(this.end===1){
      this.img = this.kartyInfo[this.numbers[this.i]].img;
      this.title = this.kartyInfo[this.numbers[this.i]].title;
      this.des = this.kartyInfo[this.numbers[this.i]].des;
      }
      this.wybor = arg;
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
    for (let i = 0; i < this.count ; i++) {
      this.numbers.push(i);
      console.log(i);
    }

    this.$root.$on("lose", arg => {
      this.end = 0;
      console.log(this.postacieInfo[arg].title);
     
      this.why=arg;
       this.title = this.postacieInfo[arg].title;
      this.des = this.postacieInfo[arg].des;
      this.title = this.postacieInfo[arg].title;
      this.img = this.postacieInfo[arg].img;
      // this.des=this.postacie.arg;
    //  this.$router.replace({name:'results', params:{years:this.years,why:arg}})
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