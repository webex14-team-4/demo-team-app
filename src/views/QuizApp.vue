<template>
  <div class="quizApp">
    <div class="question">
      <h1>{{ quizs[quizIdx].question }}</h1>
      <img :src="require(`@/assets/quiz/${quizs[quizIdx].fileName}`)" alt="" />
    </div>
    <div class="choice">
      <button
        @click="showAnswer(index)"
        v-for="(choice, index) in quizs[quizIdx].choices"
        :key="choice"
      >
        {{ choice }}
      </button>
    </div>
    <div class="answer">
      <p class="feedback">{{ feedback }}</p>
      <button :class="nextButton" @click="nextQuiz">次の問題へ進む</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quizIdx: 0,
      quizs: [
        {
          question: "世界で2番目に高い山は？",
          fileName: "K2.webp",
          choices: ["K2", "モンブラン山", "富士山"],
          correctChoiceIdx: 0,
          feedbacks: ["yes", "no", "no"],
        },
        {
          question: "世界で2番目に深い湖は？",
          fileName: "Baikal.jpg",
          choices: ["バイカル湖", "タンガニーカ湖", "カスピ海"],
          correctChoiceIdx: 1,
          feedbacks: ["no", "yes", "no"],
        },
      ],
      nextButton: "non_visible",
      feedback: "",
    }
  },
  methods: {
    showAnswer(choiceIdx) {
      this.__showFeedback(choiceIdx)
      this.__showNextButton(
        choiceIdx === this.quizs[this.quizIdx].correctChoiceIdx
      )
    },
    __showFeedback(choiceIdx) {
      this.feedback = this.quizs[this.quizIdx].feedbacks[choiceIdx]
    },
    __showNextButton(isCorrect) {
      this.nextButton = isCorrect ? "visiable" : "non_visible"
    },
    nextQuiz() {
      this.quizIdx =
        this.quizIdx === this.quizs.length - 1 ? 0 : this.quizIdx + 1
    },
  },
}
</script>

<style>
.quizApp {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.question > img {
  height: 300px;
  width: 300px;
  object-fit: contain;
}
.choice {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}

.non_visible {
  display: none;
}
.visible {
  display: block;
}
</style>
