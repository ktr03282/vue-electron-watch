<template lang="pug">
  div(v-on:click.right="showColorPicker").clock-container
    table
      tr
        th(v-for="v in clock.definition") {{v}}
      clock-table-row(title="y" v-bind:data="clock.year" v-bind:color="starColor")
      clock-table-row(title="m" v-bind:data="clock.month" v-bind:color="starColor")
      clock-table-row(title="d" v-bind:data="clock.day" v-bind:color="starColor")
      clock-table-row(title="h" v-bind:data="clock.hour" v-bind:color="starColor")
      clock-table-row(title="m" v-bind:data="clock.minute" v-bind:color="starColor")
      clock-table-row(title="s" v-bind:data="clock.second" v-bind:color="starColor")
    el-dialog(v-bind:visible.sync="dialogVisible")
      material(v-model="color" style="margin-bottom: 15px")
      el-button(@click="resetColor") reset
</template>

<script>
  import moment from 'moment'
  import ClockTableRow from './Watch/ClockTableData'
  import Material from 'vue-color/src/components/Material'

  export default {
    name: 'watch',
    data () {
      return {
        now: moment(),
        clock: {
          definition: ['', 32, 16, 8, 4, 2, 1],
          year: '',
          month: '',
          day: '',
          hour: '',
          minute: '',
          second: ''
        },
        dialogVisible: false,
        defaultColor: {hex: '#6495ED'},
        color: {hex: '#6495ED'}
      }
    },
    computed: {
      starColor: function () {
        let color = this.color.hex
        if (color.length !== 7) {
          color = this.defaultColor
        }
        return {
          color: color
        }
      }
    },
    mounted: function () {
      this.update()
      setInterval(this.update, 1000)
    },
    methods: {
      update: function () {
        this.now = moment()
        const time = this.now

        this.clock.year = this.to_b(time.format('YY'))
        this.clock.month = this.to_b(time.format('MM'))
        this.clock.day = this.to_b(time.format('DD'))
        this.clock.hour = this.to_b(time.format('HH'))
        this.clock.minute = this.to_b(time.format('mm'))
        this.clock.second = this.to_b(time.format('ss'))
      },
      to_b: function (time) {
        const length = this.clock.definition.length - 1
        return ('0'.repeat(length) + parseInt(time).toString(2))
          .substr(-length, length)
          .split('')
      },
      showColorPicker: function () {
        this.dialogVisible = !this.dialogVisible
      },
      resetColor: function () {
        this.color = this.defaultColor
      }
    },
    components: {
      Material,
      ClockTableRow
    }
  }
</script>

<style lang="sass" scoped>
  .clock-container
    margin: auto
    height: 100%
    table
      th
        text-align: center
        opacity: 1
</style>
