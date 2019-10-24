<template>
    <div class="welcome container">
      <div class="card text-white bg-dark mb-3" style="max-width: 500px; margin:0 auto;">
  <div  class="card-body">
  <h2  class="card-header">Global Counting</h2>
  <p class="card-body" >  Global Counting to gra edukacyjno-taktyczna w której wcielasz się w przywódcę nieokreślonej grupy społecznej.
      Twoim nadrzędnym zadaniem jest zapobiec wszelkim kataklizmom i konfliktom zbrojeniowym.
       Lecz uważaj! każda twoja decyzja ma znaczący wpływ na liczczniki pokazujące planowany koniec świata przedsawionych przy pomocy czterech kategorii.
       </p>
       <h4  class="card-header text-succes">Jak grać</h4>
       <div class="card-body">
         <h5 class="text-success">O co chodzi</h5>
         <p>Celem gry jest jak najdłuższe przedłużenie czasu pozostałego do katastrofy naturalnej</p>
          <p>Podczas rozgrywki będziesz miał szansę zatwierdzenia danego projektu,decyzji,wydarzenia lub odrzucenie go. Każda decyzja ma znaczący wpływ na świat gry.
W grze możemy spotkać cztery rodzaje liczników

          </p>
         <h5 class="text-success">Rodzaje liczników:</h5>
            <p>Przeludnienie &bull; klimat &bull; Polityka	&bull; Zasoby</p> 
                <font-awesome-icon style="font-size:2em; margin:20px" icon="users"/>
                <font-awesome-icon style="font-size:2em; margin:20px" icon="leaf"/>
                <font-awesome-icon style="font-size:2em; margin:20px" icon="handshake"/>
                <font-awesome-icon style="font-size:2em; margin:20px" icon="oil-can"/>
           <p>Każdy z nich reprezentuje przybliżony czas do tzw. końca świata. Czas jest liczony w latach</p> 
       </div>
  <router-link to="home">
      <button style=" margin:20px;" class="btn-primary btn-lg">Kliknij by zacząć</button>
    </router-link>
  
  </div>
  </div>
  </div>
</template>

<script>
export default {
name:'des'
}
</script>

<style>

</style>
