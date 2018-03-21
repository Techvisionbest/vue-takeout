<template>
  <div class="star" :class="starType">
    <span v-for="(itemClass,index) in itemClasses" :class="itemClass" class="star-item" :key="index"></span>
  </div>
</template>

<script>
  const LENGTH =5;
  const CLS_ON='on';
  const CLS_HALF='half';
  const CLS_OFF='off';
    export default {
        props:{
          size:{
            type:Number
          },
          score:{
            type:Number
          },
        },
      computed:{
          starType(){
            return 'star-'+this.size;
          }
      }
    }
</script>

<style scoped>

</style>
