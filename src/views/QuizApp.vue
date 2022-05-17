<!-- 
  クイズアプリの仕様

  概要：お遊び（笑）MLと人の勝負（学習済みMLを使って、クイズの正誤でMLと勝負する）

  オブジェクト：
  1. クイズのデータセット：imageNet
  2. 対戦相手：深層学習モデル
  3. プレイヤー：人
  
  機能（必要）：
  1. クイズ
  2. ランキング（DBが必要）


  概要：とりあえず最低限の機能で実装してみた。

  機能：みんなでクイズをアップロードすることができる。（dbを活用）

  TODO：dbを使わない。とりあえずソースファイル内で定義する。

-->

<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ question }}</h2>
    <img
      class="quiz-image"
      :src="require(`@/assets/quiz/${quizImg}`)"
      :alt="question"
    />
    <div class="container">
      <button @click="clickAnswer">
        {{ choices[0] }}
      </button>
      <button>
        {{ choices[1] }}
      </button>
      <button>
        {{ choices[2] }}
      </button>
    </div>
    <div :id="answerStyle">答えは{{ answer }}!!</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: "世界で2番目に高い山は？",
      quizImg: "K2.webp",
      choices: ["K2", "モンブラン山", "富士山"],
      answerStyle: "defalut_answer",
      answer: "K2",
    }
  },
  methods: {
    clickAnswer: function () {
      this.answerStyle = "visiable_answer"
    },
  },
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.quiz-image {
  height: 300px;
  width: 300px;
  object-fit: contain;
}

.container {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}

#defalut_answer {
  display: none;
}

#visiable_answer {
  display: block;
}
</style>
