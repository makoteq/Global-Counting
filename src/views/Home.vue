<template>
  <div class="home">
    <licznik/>
    <pole/>
  </div>
</template>

<script>
// @ is an alias to /src
import licznik from '@/components/licznik.vue'
import pole from '@/components/pole.vue'
export default {
  name: 'home',
  components: {
    licznik,pole
  }
}
</script>
