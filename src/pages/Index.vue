<template>
  <q-page class="flex flex-center hangman__game" v-if="page == 1">
    <div class="select__word items-center justify-center flex column">
      <div class="text-h3 q-pa-md">Jogo da Forca</div>
      <p>Escolha uma palavra para começar</p>
      <q-input
        class="full-width"
        outlined
        v-model="word"
        dense
        placeholder="Digite aqui a palavra"
      />
      <q-btn
        color="primary"
        class="q-ma-md full-width"
        label="Próximo"
        @click="page = 2"
      />
    </div>
  </q-page>
  <q-page class="flex flex-center hangman__game" v-if="page == 2">
    <div class="select__helpword items-center justify-center flex column">
      <div class="text-h3 q-pa-md">Jogo da Forca</div>
      <p>Agora, deixe uma pequena dica sobre ela</p>
      <q-input
        class="full-width"
        outlined
        v-model="word_help"
        dense
        placeholder="Digite aqui uma dica"
      />
      <q-btn
        color="primary"
        class="q-ma-md full-width"
        label="Próximo"
        @click="page = 3"
      />
    </div>
  </q-page>
  <q-page class="flex flex-center hangman__game" v-if="page == 3">
    <div class="hangman__game-start items-center justify-center flex column">
      <div class="text-h3 q-pa-md">Jogo da Forca</div>
      <p>Feito, vamos ao jogo!</p>
      <q-btn
        color="primary"
        class="q-ma-md full-width"
        label="Começar"
        @click="page = 4"
      />
    </div>
  </q-page>
  <q-page class="flex flex-center hangman__game" v-if="page == 4">
    <div class="hangman__game-start items-center justify-center flex column">
      <img
        class="hangman__game-image"
        :src="'images/game/' + errors + '.png'"
      />
      <div class="hangman__game-keyboard flex">
        <q-btn
          color="secondary"
          @click="errors < 6 ? errors++ : ''"
          class="hangman__game-keyboard-key"
          v-for="(letra, key) in 'abcçdefghijklmnopqrstuvwxyz'"
          :key="key"
        >
          {{ letra }}
        </q-btn>
      </div>
      <q-btn
        v-if="errors === 6"
        color="primary"
        class="q-ma-md"
        label="Jogar de novo"
        @click="restartGame"
      />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "PageIndex",
  setup() {
    const page = ref(4);
    const word = ref("");
    const word_help = ref("");
    const errors = ref(0);

    const restartGame = () => {
      word.value = "";
      word_help.value = "";
      errors.value = 0;
      page.value = 1;
    };
    const verifyKey = (key) => {
      if (word.value.toLowerCase().indexOf(key.toLowerCase()) >= 0) {
      } else {
        errors.value++;
      }
    };

    return {
      page,
      word,
      word_help,
      errors,
      restartGame,
      verifyKey,
    };
  },
});
</script>
<style scoped>
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
</style>
