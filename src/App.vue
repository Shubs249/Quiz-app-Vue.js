<template>
  <header class="display-3">{{ headert }}</header>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered" 
      />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/que_Questions.vue";
import Result from "./components/res_Result.vue";


export default {
  name: "App",
  components: {
    Questions,
    Result,
    
    
  },
  data() {
    return {
        headert: 'Fun Quiz',
      questionsAnswered: 0,
      totalCorrect: 0,
      //questions to be asked and their results
      questions: [
        {
          q: "What is 9 + 9?",
          answers: [
            {
              text: "18",
              is_correct: true,
            },
            {
              text: "10",
              is_correct: false,
            },
            {
              text: "19",
              is_correct: false,
            },
            {
              text: "17",
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "shubham"?',
          answers: [
            {
              text: "9",
              is_correct: false,
            },
            {
              text: "7",
              is_correct: true,
            },
            {
              text: "4",
              is_correct: false,
            },
            {
              text: "10",
              is_correct: false,
            },
          ],
        },
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              is_correct: false,
            },
            {
              text: "a",
              is_correct: true,
            },
            {
              text: "i",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  //if the question is correct then method will define it as correct else 
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style scoped>
header {
    color: red;
    margin-top: 10px;
    opacity: 25px;
    text-align: center;
    font-size: 100px;
}


</style>>
