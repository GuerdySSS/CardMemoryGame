<template lang='vue'>
  <div id="app" class="app">
    <div class="app__level">
      <div class="app__level__wrapper">
        <h4 class="app__level__wrapper__header" style='color: green' v-if="this.counterOpenedCards == 8">Вы выиграли!!!</h4>
        <h4 class="app__level__wrapper__header" style='color: red' v-if="this.attempts == 0">Вы проиграли :(</h4>
        <h4 class="app__level__wrapper__header">Выберите уровень сложности</h4>
        <div class="app__level__wrapper__lvlBlock">
          <input class="app__level__wrapper__lvlBlock__radio" value=25 checked id="easy" name="level" type="radio">
          <label class="app__level__wrapper__lvlBlock__label" for="easy">Легкий (25 попыток)</label>
        </div>
        <div class="app__level__wrapper__lvlBlock">
          <input class="app__level__wrapper__lvlBlock__radio" value=20 id="normal" name="level" type="radio">
          <label class="app__level__wrapper__lvlBlock__label" for="normal">Средний (20 попыток)</label>
        </div>
        <div class="app__level__wrapper__lvlBlock">
          <input class="app__level__wrapper__lvlBlock__radio" value=15 id="hard" name="level" type="radio">
          <label class="app__level__wrapper__lvlBlock__label" for="hard">Сложный (15 попыток)</label>
        </div>
        <div class="app__level__wrapper__btn" @click="start">Начать</div>
      </div>
    </div>
    <div class="app__header">Card Memory Game</div>
    <div class="app__panel">
      <div class="app__panel__attempts">Attempts: {{ attempts }}</div>
      <img class="app__panel__repeat" @click="start" src='https://img.icons8.com/external-dreamstale-lineal-dreamstale/15/external-repeat-music-dreamstale-lineal-dreamstale-3.png'>
    </div>
    <div class="app__wrapper">
      <button v-for="n in 16" class="app__wrapper__card" @click="cardClick(--n)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isOpenedFirstCard: false,
      selectedCard: null,
      cardValue: null,
      counterOpenedCards: null,
      attempts: null
    }
  },
  mounted() {
    this.start()
  },
  methods: {
    cardClick(x) {
      
      if (this.isOpenedFirstCard == false) { // если ни одна картонка не открыта, то выполняем
        document.getElementsByClassName('app__wrapper__card')[x].classList.toggle('app__wrapper__card_isFlipped') // переворачиваем картонку
        this.isOpenedFirstCard = true // теперь одна картонка открыта
        this.selectedCard = document.getElementsByClassName('app__wrapper__card')[x] // запоминаем какая открыта картона, если картинка на этой не совпадет с картинкой на след, то закрываем
        this.cardValue = document.getElementsByClassName('app__wrapper__card__face_back')[x] // запоминаем картинку для сравнения
      }
      else {
        document.getElementsByClassName('app__wrapper__card')[x].classList.toggle('app__wrapper__card_isFlipped') // если картонка открыта, то выполняем
        // document.querySelectorAll('app__wrapper__card').setAttribute('disabled')
        if (this.cardValue.innerHTML != document.getElementsByClassName('app__wrapper__card__face_back')[x].innerHTML) { // если картинка на 1 картонке не совпадает, то выполняем
          this.attempts -= 1 // забираем одну попытку
          if (this.attempts < 11 && this.attempts > 5) document.getElementsByClassName('app__panel__attempts')[0].classList.add('app__panel__attempts_orange') // просто смена цвета в
          else if (this.attempts < 6 && this.attempts > 0) document.getElementsByClassName('app__panel__attempts')[0].classList.add('app__panel__attempts_red') // зависимости от количества
          else if (this.attempts == 0) document.getElementsByClassName('app__level')[0].classList.toggle('app__level_close') // попыток и открываем диалоговое окно с поражением, если их нет
          setTimeout(() => {
            this.selectedCard.classList.toggle('app__wrapper__card_isFlipped')
            document.getElementsByClassName('app__wrapper__card')[x].classList.toggle('app__wrapper__card_isFlipped') // переворачиваем рубашкой вверх 2 картонку
          }, 700);
        }
        else {
          setTimeout(() => {
            this.cardValue.classList.add('app__wrapper__card__face_back_active') // меняем состояние 1 картонки на угаданную
            document.getElementsByClassName('app__wrapper__card__face_back')[x].classList.add('app__wrapper__card__face_back_active') // меняем состояние 2 картонки на угаданную
          }, 700);
          this.counterOpenedCards += 1 // увеличиваем счетчик угаданных карт для определения победы
          if (this.counterOpenedCards == 8) document.getElementsByClassName('app__level')[0].classList.toggle('app__level_close') // открываем диалоговое окно с победой
        }
        setTimeout(() => {
          this.isOpenedFirstCard = false // чистка
          this.selectedCard = null // всех
          this.cardValue = null // переменных
          // document.querySelectorAll('app__wrapper__card').removeAttribute('disabled')
        }, 700);
      }
    },
    start() {
      let mass = ["<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/vk-circled.png'>", // массив с картинками
      "<img class='imgCard' src='https://img.icons8.com/material-outlined/30/instagram-new--v1.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/facebook-new.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-filled/30/tiktok--v1.png'>",
      "<img class='imgCard' src='https://img.icons8.com/material-outlined/30/telegram-app.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/viber.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/twitter-circled--v1.png'>",
      "<img class='imgCard' src='https://img.icons8.com/material-outlined/30/snapchat.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/vk-circled.png'>",
      "<img class='imgCard' src='https://img.icons8.com/material-outlined/30/instagram-new--v1.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/facebook-new.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-filled/30/tiktok--v1.png'>",
      "<img class='imgCard' src='https://img.icons8.com/material-outlined/30/telegram-app.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/viber.png'>",
      "<img class='imgCard' src='https://img.icons8.com/ios-glyphs/30/twitter-circled--v1.png'>",
      "<img class='imgCard' src='https://img.icons8.com/material-outlined/30/snapchat.png'>"]
      
      for (let i=0; i<=15; i++) {
        document.getElementsByClassName('app__wrapper__card')[i].classList.remove('app__wrapper__card_isFlipped') // переворачиваем все картонки
        document.getElementsByClassName('app__wrapper__card__face_back')[i].classList.remove('app__wrapper__card__face_back_active') // меняем состояние картонок на не угаданные
        let rnd = Math.floor(Math.random() * (mass.length - 1)); // берем случайную картинку
        document.getElementsByClassName('app__wrapper__card__face_back')[i].innerHTML = mass[rnd] // помещаем картинку в картонку
        mass.splice(rnd, 1) // удаляем картинку, чтобы не было повторений
      }
      document.getElementsByClassName('app__level')[0].classList.toggle('app__level_close') // открываем диалоговое окно
      this.attempts = document.querySelector('input[name="level"]:checked').value // выбранные попытки из диалогового окна будут отображаться над полем с картонками
      document.getElementsByClassName('app__panel__attempts')[0].classList.remove('app__panel__attempts_orange') // делаем состояние строки попыток дефолтным
      document.getElementsByClassName('app__panel__attempts')[0].classList.remove('app__panel__attempts_red') // тут тоже
    }
  }
}
</script>

<style scoped lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');

  .app {
    width: fit-content;
    margin: 0 auto;

    &__header {
      text-align: center;
      color: grey;
      font-size: 30px;
      margin: 20px 0;
      font-family: 'Roboto', sans-serif;
      font-weight: bolder;

      @media (max-width: 540px) {
        font-size: 20px;
      }
    }

    &__panel {
      justify-content: center;
      display: flex;
      justify-content: space-between;

      &__attempts {
        font-family: 'Roboto', sans-serif;
        font-size: 20px;
        color: darkgreen;
        font-weight: bold;

        @media (max-width: 540px) {
          font-size: 15px;
        }

        &_orange {
          color: orange;
        }

        &_red {
          color: red;
        }
      }

      &__repeat {
        cursor: pointer;
        width: 15px;
        height: 15px;
        margin-top: 5px;

        @media (max-width: 540px) {
          width: 10px;
          height: 10px;
        }
      }
    }

    &__wrapper {
      display: grid;
      grid-template-columns: 100px 100px 100px 100px;
      background: linear-gradient(160deg, #26c6da, 50%, #ab47bc);
      padding: 25px;
      width: fit-content;
      margin: 10px auto;
      border-radius: 10px;
      box-shadow: 10px 10px 10px rgba(0,0,0,0.5);
      grid-gap: 20px;

      @media (max-width: 540px) {
        grid-template-columns: 50px 50px 50px 50px;
        padding: 15px;
        grid-gap: 10px;
      }

      &__card {
        width: 100px;
        height: 100px;
        transition: transform 1s;
        transition: 1s;
        transform-style: preserve-3d;
        cursor: pointer;
        user-select: none;
        border-radius: 10px;
        border: none;

        @media (max-width: 540px) {
          width: 50px;
          height: 50px;
        }

        &_isFlipped {
          transform: rotateY(180deg);
          pointer-events: none;
        }

        &__face {
          position: absolute;
          width: 100px;
          height: 100px;
          line-height: 100px;
          color: white;
          text-align: center;
          font-size: 40px;
          border-radius: 10px;
          backface-visibility: hidden;

          @media (max-width: 540px) {
            width: 50px;
            height: 50px;
            line-height: 43px;
          }

          &_front {
            background: rgba(40, 53, 64, 100);
          }

          &_back {
            background: #00A1F1;
            transform: rotateY(180deg);
            box-shadow: 0 0 10px rgba(0,0,0,0.5);

            &_active {
              transition: 1s;
              background: #0AFF47;
            }
          }
        }
      }
    }

    &__level {
      z-index: 10;
      width: 100%;
      height: 100%;
      background: rgba(13, 13, 13, 0.7);
      position: absolute;
      display: none;
      justify-content: center;

      &_close {
        display: flex;
      }

      &__wrapper  {
        background-color: #eeeeee;
        height: fit-content;
        border-radius: 30px;
        padding: 20px;
        margin-top: 245px;

        @media (max-width: 540px) {
          margin-top: 100px;
        }

        &__header {
          font-family: 'Roboto', sans-serif;
          margin-bottom: 20px;
          text-align: center;

          @media (max-width: 540px) {
            font-size: 14px;
          }
        }

        &__lvlBlock {
          margin-bottom: 10px;

          &__radio {
            cursor: pointer;
            width: 20px;
            position: relative;

            @media (max-width: 540px) {
              top: 2px;
            }
          }

          &__label {
            font-family: 'Roboto', sans-serif;
            cursor: pointer;
            color: #424242;
            font-weight: bold;

            @media (max-width: 540px) {
              font-size: 12px;
            }
          }
        }

        &__btn {
          font-family: 'Roboto', sans-serif;
          cursor: pointer;
          border: 1px solid #00A1F1;
          text-align: center;
          color: #00A1F1;
          transition: 1s;

          @media (max-width: 540px) {
            font-size: 14px;
          }

          &:hover {
            color: white;
            background: #00A1F1;
          }
        }
      }
    }
  }
</style>