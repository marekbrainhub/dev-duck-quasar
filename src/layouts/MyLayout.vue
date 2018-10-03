<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-header>
      <q-toolbar color="primary">
        <q-toolbar-title center>
          Super Timer
          <div slot="subtitle">Running on Quasar v{{ $q.version }}</div>
        </q-toolbar-title>

        <q-btn flat round dense icon="brush">
          <q-popover>
            <q-color-picker v-model="color"></q-color-picker>
          </q-popover>
        </q-btn>
      </q-toolbar>
    </q-layout-header>

    <q-page-container>
      <div class="flex column justify-center items-center absolute-center">
        <q-knob
          v-model="count"
          color="primary"
          readonly
          :min=0
          :max="max"
        />

        <q-input
          type="number"
          v-model="max"
          class="q-ma-md"
          placeholder="Seconds"
        />

        <div class="flex">
          <q-btn color="primary" class="q-mx-md" @click="startTimer(max)">Start</q-btn>
          <q-btn class="q-mx-md" @click="stopTimer()">Stop</q-btn>
        </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import { colors } from 'quasar'

export default {
  name: 'MyLayout',
  data: () => ({
    color: '#FF00FF',
    max: null,
    count: 0,
    timer: null
  }),
  methods: {
    startTimer: function (value) {
      clearInterval(this.timer)
      this.count = this.max

      const that = this

      this.timer = setInterval(function () {
        that.count--
        if (that.count <= 0) {
          that.stopTimer()
        }
      }, 1000)
    },
    stopTimer: function (value) {
      this.count = 0
      clearInterval(this.timer)
    }
  },
  watch: {
    color: (newColor) => colors.setBrand('primary', newColor)
  }
}
</script>
