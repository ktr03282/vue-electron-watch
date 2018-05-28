<template lang="pug">
  tr
    td {{title}}
    td(v-for="v in data")
      i(v-if="v === '0'").el-icon-star-off.star.off
      i(v-else  v-bind:style="color").el-icon-star-on.star.on
</template>

<script>
  export default {
    name: 'clock-table-row',
    props: ['title', 'data', 'color']
  }
</script>

<style lang="sass" scoped>
  td
    i
      font-size: 2em
    .star
      transition-property: color, -webkit-transform
      transition-duration: 1s

    .star.on
      /*color: cornflowerblue*/
      -webkit-transform: rotate(0deg)

    .star.off
      color: #444
      -webkit-transform: rotate(360 - 72deg)
</style>
