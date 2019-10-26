<template>
  <div class="welcome">
    <des/>
    </div>
</template>

<script>
import des from '@/components/des.vue'
export default {
  name:'welcome',
    components: {
    des
  },
  mounted () {
    if (this.$route.params.res==1){
      location.reload();
      console.log('elo');
    }
      console.log('elo');
  },


}
</script>

<style>

</style>
