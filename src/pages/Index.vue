<template>
  <q-page class="flex flex-center bg-white hangman__game" v-if="page == 1">
    <div class="select__word items-center justify-center flex column">
      <Header subtitle="Escolha uma palavra para começar" />
      <q-input
        class="full-width"
        outlined
        v-model="word"
        dense
        placeholder="Digite aqui a palavra"
      />

      <q-btn
        :disable="!word.length"
        color="primary"
        class="q-ma-md full-width"
        label="Próximo"
        @click="page = 2"
      />
      Ou
      <q-btn
        color="primary"
        class="q-ma-md full-width"
        label="Uma palavra surpresa!"
        @click="setRamdomWord()"
      />
    </div>
  </q-page>
  <q-page class="flex flex-center bg-white hangman__game" v-if="page == 2">
    <div class="select__helpword items-center justify-center flex column">
      <Header subtitle="Agora, deixe uma pequena dica sobre ela" />
      <q-input
        class="full-width"
        outlined
        v-model="word_help"
        dense
        placeholder="Digite aqui uma dica"
      />
      <q-btn
        :disable="!word_help.length"
        color="primary"
        class="q-ma-md full-width"
        label="Próximo"
        @click="page = 3"
      />
    </div>
  </q-page>
  <q-page class="flex flex-center bg-white hangman__game" v-if="page == 3">
    <div class="hangman__game-start items-center justify-center flex column">
      <Header subtitle="Feito, vamos ao jogo!" />
      <q-btn
        color="primary"
        class="q-ma-md full-width"
        label="Começar"
        @click="startGame"
      />
    </div>
  </q-page>
  <q-page class="flex flex-center bg-white hangman__game" v-if="page == 4">
    <div class="hangman__game-start items-center justify-center flex column">
      <img
        class="hangman__game-image"
        :src="'images/game/' + errors + '.png'"
      />
      <div class="text-center">
        <h4 class="q-pa-none q-ma-none">{{ answer.join(" ") }}</h4>
        <p class="q-pa-none q-ma-none"><b>Dica:</b> {{ word_help }}</p>
      </div>
      <div class="hangman__game-keyboard flex">
        <q-btn
          color="secondary"
          @click="verifyLetter(letra)"
          class="hangman__game-keyboard-key"
          v-for="(letra, key) in letters_game"
          :key="key"
        >
          {{ letra }}
        </q-btn>
      </div>
      <q-btn
        v-if="errors === 6"
        color="primary"
        class="q-ma-md"
        label="Game over.. jogar de novo?"
        @click="restartGame"
      />
    </div>
  </q-page>
  <q-page
    class="flex flex-center bg-white hangman__game-sucess-page"
    v-if="page == 5"
  >
    <div
      class="hangman__game-sucess q-pa-lg items-center justify-center flex column"
    >
      <img src="/images/emoji-party.gif" class="hangman__game-sucess-image" />
      <div class="text-h3 q-pa-md">Parabéns!</div>
      <p class="q-pa-none q-ma-none">A palavra era</p>
      <h6 class="q-pa-none q-ma-none">{{ word }}</h6>
      <p class="q-pa-none q-ma-none">
        Você conseguiu descobrir a palavra secreta. Que tal jogar de novo?
      </p>
      <q-btn
        color="primary"
        class="q-ma-md"
        label="Jogar de novo"
        @click="restartGame"
      />
    </div>
  </q-page>
</template>

<script>
import Header from "src/components/Parts/Header.vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "PageIndex",
  components: { Header },
  setup() {
    const page = ref(1);
    const word = ref("");
    const word_help = ref("");
    const errors = ref(0);
    const answer = ref("");
    const letters_game = ref("abcçdefghijklmnopqrstuvwxyz");
    const letters = ref("abcçdefghijklmnopqrstuvwxyz");

    const startGame = () => {
      word.value = word.value.replace(/\s/g, "");
      answer.value = Array(word.value.length).fill("_");
      page.value = 4;
    };

    const restartGame = () => {
      word.value = "";
      word_help.value = "";
      errors.value = 0;
      page.value = 1;
      letters_game.value = letters.value;
    };

    const setRamdomWord = () => {
      word.value = "";
      word_help.value = "";
      errors.value = 0;
      page.value = 1;
    };

    setRamdomWord;

    const verifyLetter = (letter) => {
      let letter_position = word.value
        .toLowerCase()
        .indexOf(letter.toLowerCase());
      if (letter_position >= 0 && errors.value < 6) {
        [...word.value.toLowerCase()].forEach((value, key) => {
          if (value === letter) answer.value[key] = value;
        });
        verifyWinner();
      } else {
        errors.value < 6 ? errors.value++ : "";
      }
      letters_game.value = letters_game.value.replace(letter, "");
    };

    const verifyWinner = () => {
      word.value.toLowerCase() === answer.value.join("")
        ? (page.value = 5)
        : "";
    };

    return {
      page,
      word,
      word_help,
      errors,
      letters,
      letters_game,
      answer,
      startGame,
      setRamdomWord,
      restartGame,
      verifyLetter,
      verifyWinner,
    };
  },
});
</script>
<style scoped>
.hangman__game-logo {
  width: 300px;
}
.hangman__game-image {
  width: 300px;
}
.hangman__game-keyboard {
  max-width: 80%;
  justify-content: center;
}
.hangman__game-keyboard-key {
  margin: 5px;
}
.hangman__game-sucess-page {
  background-size: cover;
  background-repeat: no-repeat;
}
.hangman__game-sucess {
  background-color: #ffffffeb;
}
.hangman__game-sucess-image {
  width: 170px;
}
</style>
