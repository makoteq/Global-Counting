<template>
  <div class="results">
    <h2>Wyniki</h2>
    <div class="container">
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
      <td class="text-success" >Coming soon!</td>
      <td class="text-danger" >{{why}}</td>
    </tr>
  </tbody>
</table>
</div>
<div class="card text-white bg-dark mb-3" style="max-width: 500px; margin:0 auto;">
  <div class="card-body">
  <h3 class="card-header">Chcesz Działać?</h3>
  <p class="card-body">Sprawdź poniższe linki by dowiedzic się więcej!</p>
  <a  href="https://www.greenpeace.org/poland/" target="_blank">Greenpeace</a><br>
  <a href="https://www.wwf.pl/" target="_blank">WWF</a><br>
  <a href="https://www.foei.org/" target="_blank">Friends of the Earth International</a>
  </div>
</div>

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
           this.why='Klęska Żywiołowa ogarniająca cały świat'
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

