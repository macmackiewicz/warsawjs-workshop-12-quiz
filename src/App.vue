<template>
  <v-app dark>
    <v-content>
      <v-container>
        <v-layout row justify-center>
          <v-flex md6 xs10>
            <v-card>
              <img src="./assets/millionaire.png" width="100%">
              <div v-if="hasUserWon">
                <v-card-text class="headline">
                  <p class="text-xs-center">Gratulacje, wygrałeś $1 000 000!</p>
                </v-card-text>
              </div>
              <div v-else>
                <v-card-title class="title pb-0">
                  {{currentQuestion.title}}
                </v-card-title>
                <v-card-text>
                  <v-list>
                    <v-list-tile v-for="(answer, answerIndex) in currentQuestion.answers"
                                 :key="answerIndex"
                                 @click="selectAnswer(answerIndex)"
                                 :class="getAnswerStatus(answerIndex)"
                      >
                        {{answer}}
                    </v-list-tile>
                  </v-list>
                </v-card-text>
                <v-card-actions>
                  <v-btn block v-if="isUserCorrect" @click="nextQuestion">
                    Następne pytanie
                  </v-btn>
                  <v-btn block v-else-if="userAnswer !== null"
                         @click="restartQuiz"
                  >
                    Zacznij od początku
                  </v-btn>
                </v-card-actions>
              </div>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import {quiz} from './quiz'

export default {
  data () {
    return {
      currentQuestionIndex: 0,
      userAnswer: null
    }
  },
  computed: {
    currentQuestion () {
      return quiz[this.currentQuestionIndex]
    },
    isUserCorrect () {
      return this.currentQuestion.correctAnswerIndex === this.userAnswer
    },
    hasUserWon () {
      return quiz.length === this.currentQuestionIndex
    }
  },
  methods: {
    getAnswerStatus (answerIndex) {
      if (this.currentQuestion.correctAnswerIndex === answerIndex && answerIndex === this.userAnswer) {
        return 'success'
      } else if (this.userAnswer === answerIndex) {
        return 'error'
      } else {
        return 'secondary'
      }
    },
    selectAnswer (answerIndex) {
      if (this.userAnswer === null) {
        this.userAnswer = answerIndex
      }
    },
    nextQuestion () {
      this.userAnswer = null
      this.currentQuestionIndex++
    },
    restartQuiz () {
      this.userAnswer = null
      this.currentQuestionIndex = 0
    }
  }
}
</script>
