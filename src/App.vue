<script setup>
  import Card from './components/Card.vue';
</script>

<template>
  <div class="bg-gray h-screen flex flex-col items-start">
    <p class="mx-auto text-10 font-800 border-rounded-1 sm:mt-24 mt-10">
      Card Generator
    </p>
    <div class="mx-auto">
      <div class="sm:flex bg-white px-5 py-3 border-rounded w-fit h-fit">
        <div class="flex items-center my-1">
          <span>Generate</span>
          <input type="text" class="w-10 h-8 border-1 text-center mx-2" v-model="xVal" @input="$emit('update:xVal', $event.target.value)"/>
          <span>rabdiom cards,</span>
        </div>
        <div class="flex items-center my-1">
          <span class="sm:ml-2">each with</span>
          <input type="text" class="w-10 h-8 border-1 text-center mx-2" v-model="yVal" @input="$emit('update:yVal', $event.target.value)" />
          <span>row/columns</span>
        </div>
        <button :class="[disabled ? 'bg-blue-200 hover:bg-blue-300 p-2 text-white border rounded sm:ml-5 w-full sm:w-auto': 'bg-blue-400 hover:bg-blue-500 p-2 text-white border rounded sm:ml-5 w-full sm:w-auto']" @click="handleInput" :disabled="disabled">
          Generate
        </button>
      </div>
      <p v-if="error" class="bg-red-4 px-5 py-2 text-white text-3 font-600 border-rounded-1 my-2">
        {{error}}
      </p>
    </div>
    <div class="border-3 w-fit h-fit mx-auto mt-20">
      <Card :xVal="xVal" :yVal="yVal" :wf="wf"/>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        error: null,
        disabled: false,
        xVal: 5,
        yVal: 5,
        wf: 0,
      };
    },
    methods: {
      handleInput:function(){
        this.wf = Math.random();
      }
    },
    mounted() {
      this.handleInput()
    },
    watch: {
      xVal: function() {
        if ( isNaN(this.xVal) ){
            this.error = "Invalid number.";
            this.disabled = true;
        }else{
          if ( this.xVal < 1 || this.xVal > 5 ){
            this.error = "Value must be 1 between 5.";
            this.disabled = true;
          } else {
            this.error = null;
            this.disabled = false;
            this.handleInput();
          }
        }
      },
      yVal: function() {
        if ( isNaN(this.yVal) ){
            this.error = "Invalid number.";
            this.disabled = true;
        }else{
          if ( this.yVal < 1 || this.yVal > 5 ){
            this.error = "Value must be 1 between 5.";
            this.disabled = true;
          } else {
            this.error = null;
            this.disabled = false;
            this.handleInput();
          }
        }
        this.handleInput();
      }
    },
  };
</script>

<style scoped>
</style>
