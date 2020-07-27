<template>
  <div>
    <p>
      <button
        @click="isMulti = !isMulti"
        v-text="isMulti ? 'かける' : 'わる'"
      />
    </p>
    <p>{{ dataA }} {{ isMulti ? '×' : '÷' }} {{ dataB }} = {{ calcData }}</p>
    <p><button @click="addNum(calcData)" v-text="'加算'" /></p>
    <p>加算結果：{{ clickNum }}</p>
  </div>
</template>
<script lang="ts">
import Vue from 'vue'

interface LocalData {
  isMulti: boolean
  clickNum: number
  dataA: number
  dataB: number
}

export default Vue.extend({
  data(): LocalData {
    return {
      isMulti: false,
      clickNum: 0,
      dataA: 6,
      dataB: 3,
    }
  },
  computed: {
    calcData(): number {
      return this.isMulti ? this.dataA * this.dataB : this.dataA / this.dataB
    },
  },
  mounted() {
    this.isMulti = true
  },
  methods: {
    addNum(addValue: number) {
      this.clickNum += addValue
    },
  },
})
</script>
