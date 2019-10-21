<template>
  <div class="results">
    <h2>Wyniki</h2>
    <table class="table table-striped table-dark">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Lata</th>
      <th scope="col">Czas</th>
      <th scope="col">Przyczyna Kataklzmu</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td class="text-warning" >{{years}}</td>
      <td class="text-success" > {{time}}</td>
      <td class="text-danger" >{{why}}</td>
    </tr>
  </tbody>
</table>
  </div>
</template>
<script>
export default {
  name:'results',
  data() {
    return {
      years:'',
      time:0,
      why:''
    }
  },
  mounted(){
    this.years=this.$route.params.years
    switch(this.$route.params.why){
      case 0:
        this.why='Przeludnienie'
        break;
         case 1:
           this.why='Przegrzanie planety'
        break;
         case 2:
           this.why='Wojny, aspekty polityczne'
        break;
         case 3:
             this.why='Wyeksplatowane zasoby naturalne'
        break;
        default:
    }
  //  this.years=this.$route.params.years
  }
}
</script>

