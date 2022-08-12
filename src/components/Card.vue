<script setup>

</script>
<template>
  <div v-for="(val, index) in cards" :key="index">
    <div v-for="(valss, v_index) in val" :key="v_index" class="bg-white border-3 inline-grid text-center text-size-4xl font-bold w-16 h-16">
      {{valss}}
    </div>
  </div>
</template>

<script>
export default {
  props: ['xVal', 'yVal', 'wf'],
  data() {
    return {
      cards: []
    }
  },
  watch: { 
    wf: function() {
      var result           = [];
      var chars       = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      var length = this.xVal * this.yVal;
      var chunk = [];
      for ( var i = 0; i < length; i++ ) {
        var rand = chars.charAt(Math.floor(Math.random() * chars.length));
        chars = chars.replace(rand, '');
        chunk.push(rand);
        if ( chunk.length == this.xVal ){
          result.push(chunk);
          chunk = [];
        }
      }
      this.cards = result;
    }
  }
}
</script>

<style scoped>
</style>
