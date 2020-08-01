<template>
  <div>
    <p>
      <button
        @click="state.isMulti = !state.isMulti"
        v-text="state.isMulti ? 'かける' : 'わる'"
      />
    </p>
    <p>
      {{ state.dataA }} {{ state.isMulti ? '×' : '÷' }} {{ state.dataB }} =
      {{ calcData }}
    </p>
    <p><button @click="addNum" v-text="'加算'" /></p>
    <p>加算結果：{{ state.clickNum }}</p>
  </div>
</template>
<script lang="ts">
import {
  defineComponent,
  reactive,
  computed,
  onMounted,
} from '@vue/composition-api'

export default defineComponent({
  setup() {
    const state = reactive<{
      isMulti: boolean
      clickNum: number
      dataA: number
      dataB: number
    }>({
      isMulti: false,
      clickNum: 0,
      dataA: 6,
      dataB: 3,
    })

    const calcData = computed(() => {
      return state.isMulti
        ? state.dataA * state.dataB
        : state.dataA / state.dataB
    })

    onMounted(() => {
      state.isMulti = true
    })

    const addNum = () => (state.clickNum += calcData.value)

    return { state, calcData, addNum }
  },
})
</script>
