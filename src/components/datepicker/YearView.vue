<template>
  <table role="grid" style="width: 100%">
    <thead>
    <tr>
      <td>
        <button type="button" class="btn btn-default btn-sm btn-block" style="border: none" @click="goPrevYear">
          <i class="glyphicon glyphicon-chevron-left"></i>
        </button>
      </td>
      <td colspan="3">
        <button type="button" class="btn btn-default btn-sm btn-block" style="border: none">
          <b>{{yearStr}}</b>
        </button>
      </td>
      <td>
        <button type="button" class="btn btn-default btn-sm btn-block" style="border: none" @click="goNextYear">
          <i class="glyphicon glyphicon-chevron-right"></i>
        </button>
      </td>
    </tr>
    </thead>
    <tbody>
    <tr v-for="row in rows">
      <td v-for="year in row" width="20%">
        <button type="button"
                class="btn btn-default btn-sm btn-block" style="border: none"
                :class="getBtnClass(year)"
                @click="changeView(year)">
          <span>{{year}}</span>
        </button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>
  export default {
    props: ['year'],
    computed: {
      rows () {
        let rows = []
        let yearGroupStart = this.year - this.year % 20
        for (let i = 0; i < 4; i++) {
          rows.push([])
          for (let j = 0; j < 5; j++) {
            rows[i].push(yearGroupStart + i * 5 + j)
          }
        }
        return rows
      },
      yearStr () {
        let start = this.year - this.year % 20
        return `${start} ~ ${start + 19}`
      }
    },
    methods: {
      getBtnClass (year) {
        if (year === this.year) {
          return {'btn-primary': true}
        } else {
          return {'btn-default': true}
        }
      },
      goPrevYear () {
        this.$emit('year-change', this.year - 20)
      },
      goNextYear () {
        this.$emit('year-change', this.year + 20)
      },
      changeView (year) {
        this.$emit('year-change', year)
        this.$emit('view-change', 'm')
      }
    }
  }
</script>
