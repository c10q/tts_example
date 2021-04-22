<template>
  <el-container>
    <el-card style="width: 800px">
      <el-input placeholder="텍스트 입력" v-model="text"></el-input>

      <el-divider></el-divider>

      <span>속도</span>
      <el-slider :min=1 :max=200 :format-tooltip="formatTooltip" v-model="rate" show-input></el-slider>

      <span>음높이</span>
      <el-slider :min=0 :max=2 v-model="pitch" :step=1 show-stops show-input></el-slider>

      <el-button type="primary" @click="speak">말하기</el-button>

    </el-card>
  </el-container>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      lang: 'ko-KR',
      text: '',
      rate: 10,
      pitch: 1,
    }
  },
  created() {

  },
  methods: {
    speak() {
      const speechMessage = new SpeechSynthesisUtterance()
      speechMessage.lang = this.lang
      speechMessage.text = this.text
      speechMessage.rate = this.rate / 10
      speechMessage.pitch = this.pitch

      window.speechSynthesis.speak(speechMessage)
    },
    formatTooltip(val) {
      return val / 10
    }
  }
}
</script>

