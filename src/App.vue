<template>
  <h1 class="h1 display-4 text-dark my-3 text-center text-uppercase">
    Let's make an alpaca
  </h1>

  <div class="container d-md-flex flex-row md:flex-column mt-5 pt-5">
    <div class="alpaca flex-fill position-relative">
      <img
        class="img-fluid position-absolute"
        :src="`/Alpaca/assets/backgrounds/${currentSettingValue.Backgrounds}.png`"
        alt="background"
      />
      <img
        class="img-fluid"
        :src="`/Alpaca/assets/ears/${currentSettingValue.Ears}.png`"
        alt="Ears"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/hair/${currentSettingValue.Hair}.png`"
        alt="Hair"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/neck/${currentSettingValue.Neck}.png`"
        alt="Neck"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/eyes/${currentSettingValue.Eyes}.png`"
        alt="Eyes"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/nose/${currentSettingValue.Nose}.png`"
        alt="Nose"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/mouth/${currentSettingValue.Mouth}.png`"
        alt="Mouth"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/leg/${currentSettingValue.Leg}.png`"
        alt="Leg"
      />
      <img
        class="img-fluid position-absolute start-0"
        :src="`/Alpaca/assets/accessories/${currentSettingValue.Accessories}.png`"
        alt="Accessories"
      />
    </div>

    <div class="config d-flex flex-column flex-fill p-3">
      <div class="d-flex justify-content-between align-items-center">
        <h2 class="text-dark ps-1">Customize your Alpaca</h2>
        <span
          class="badge fs-4"
          :style="{
            background: colorMap[currentSettingValue['Backgrounds']],
            cursor: 'pointer',
          }"
          title="Download"
          @click="saveSnap()"
          >⭳</span
        >
      </div>
      <div class="options mt-3">
        <button
          v-for="key in Object.keys(config)"
          :key="key"
          class="btn btn-primary px-3 m-1"
          :style="{
            background: colorMap[currentSettingValue['Backgrounds']],
            border: 0,
          }"
          @click="currentSetting = key"
        >
          {{ key }}
        </button>
      </div>
      <hr class="my-3 text-secondary" />
      <div class="option-values">
        <h3 class="h3 text-dark ps-1">{{ currentSetting }}</h3>

        <button
          v-for="key in Object.values(config[currentSetting])"
          :key="key"
          class="btn btn-outline-secondary px-3 m-1 mt-3"
          :class="{ active: currentSettingValue[currentSetting] === key }"
          @click="currentSettingValue[currentSetting] = key"
        >
          {{ key }}
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.alpaca {
  flex: 1 !important;
}
.config {
  flex: 2 !important;
}
</style>

<script>
import { config, defaultSettingValues } from './alpaca.config'
import colorMap from './colorMap'
import html2canvas from 'html2canvas'

export default {
  data() {
    return {
      config: config,
      currentSetting: 'Backgrounds',
      currentSettingValue: defaultSettingValues,
      colorMap,
    }
  },
  methods: {
    async saveSnap() {
      const alpaca = document.querySelector('.alpaca')
      const a = document.createElement('a')
      const canvas = await html2canvas(alpaca)

      a.href = canvas.toDataURL('image/png')
      a.download = 'alpaca.png'

      a.click()
    },
  },
}
</script>
