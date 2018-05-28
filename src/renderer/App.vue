<template lang="pug">
  div#app
    el-container
      router-view
</template>

<script>
  export default {
    name: 'vue-electron-watch'
  }
</script>

<style lang="sass">
  html
    width: 100%
    height: 100%
    body
      height: 100%
      font-family: "Source Han Code JP", "Ricty Diminished", sans-serif
      color: #ccc
      background-color: rgba(24, 24, 24, 0.4)
      opacity: 0.8
      -webkit-app-region: drag
      -webkit-user-select: none
      display: flex
      align-items: center
      justify-content: center
    ul
      padding: 10px
      list-style-type: none
      overflow: scroll
      li
        padding-bottom: 5px
</style>
