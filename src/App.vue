<template>
  <div id="app" class="app">
    <div class="app__level">
      <div class="app__level__wrapper">
        <h4 class="app__level__wrapper__header">Выберите уровень сложности</h4>
        <div class="app__level__wrapper__lvlBlock">
          <input class="app__level__wrapper__lvlBlock__radio" value=20 checked id="easy" name="level" type="radio">
          <label class="app__level__wrapper__lvlBlock__label" for="easy">Легкий (20 попыток)</label>
        </div>
        <div class="app__level__wrapper__lvlBlock">
          <input class="app__level__wrapper__lvlBlock__radio" value=15 id="normal" name="level" type="radio">
          <label class="app__level__wrapper__lvlBlock__label" for="normal">Средний (15 попыток)</label>
        </div>
        <div class="app__level__wrapper__lvlBlock">
          <input class="app__level__wrapper__lvlBlock__radio" value=10 id="hard" name="level" type="radio">
          <label class="app__level__wrapper__lvlBlock__label" for="hard">Сложный (10 попыток)</label>
        </div>
        <div class="app__level__wrapper__lvlBlock__btn" @click="mix">Начать</div>
      </div>
    </div>
    <div class="app__header">Card Memory Game</div>
    <div class="app__panel">
      <div class="app__panel__attempts">Attempts: {{ attempts }}</div>
      <img class="app__panel__repeat" @click="mix" src='https://img.icons8.com/external-dreamstale-lineal-dreamstale/15/external-repeat-music-dreamstale-lineal-dreamstale-3.png'>
    </div>
    <div class="app__wrapper">
      <div class="app__wrapper__card" @click="cardClick(0)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(1)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(2)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(3)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>


      <div class="app__wrapper__card" @click="cardClick(4)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(5)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(6)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(7)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>


      <div class="app__wrapper__card" @click="cardClick(8)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(9)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(10)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(11)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>


      <div class="app__wrapper__card" @click="cardClick(12)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(13)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(14)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back"></div>
      </div>
      <div class="app__wrapper__card" @click="cardClick(15)">
        <div class="app__wrapper__card__face app__wrapper__card__face_front"></div>
        <div class="app__wrapper__card__face app__wrapper__card__face_back">
          <img src='https://img.icons8.com/material-outlined/30/instagram-new--v1.png'>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      flag: false,
      item: null,
      value: null,
      counter: 0,
      attempts: null
    }
  },
  mounted() {
    this.start()
  },
  methods: {
    cardClick(x) {
      if (this.flag == false) {
        document.getElementsByClassName('app__wrapper__card')[x].classList.toggle('app__wrapper__card_isFlipped')
        this.flag = true
        this.item = document.getElementsByClassName('app__wrapper__card')[x]
        this.value = document.getElementsByClassName('app__wrapper__card__face_back')[x]
      }
      else {
        document.getElementsByClassName('app__wrapper__card')[x].classList.toggle('app__wrapper__card_isFlipped')
        if (this.value.innerHTML != document.getElementsByClassName('app__wrapper__card__face_back')[x].innerHTML) {
          this.attempts -= 1
          if (this.attempts == 0) {
            console.log('Game Over!')
          }
          setTimeout(() => {
            this.item.classList.toggle('app__wrapper__card_isFlipped')
            document.getElementsByClassName('app__wrapper__card')[x].classList.toggle('app__wrapper__card_isFlipped')
            this.flag = false
            this.item = null
            this.value = null
          }, 700);
        }
        else {
          setTimeout(() => {
            this.value.classList.add('app__wrapper__card__face_back_active')
            document.getElementsByClassName('app__wrapper__card__face_back')[x].classList.add('app__wrapper__card__face_back_active')
            this.counter += 1
            this.flag = false
            this.item = null
            this.value = null
            if (this.counter == 8) console.log('Win!')
          }, 700);
        }
      }
    },
    start() {
      document.getElementsByClassName('app__level')[0].classList.toggle('app__level_close')
    },
    mix() {
      let mass = ["<img src='https://img.icons8.com/ios-glyphs/30/vk-circled.png'>",
      "<img src='https://img.icons8.com/material-outlined/30/instagram-new--v1.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/facebook-new.png'>",
      "<img src='https://img.icons8.com/ios-filled/30/tiktok--v1.png'>",
      "<img src='https://img.icons8.com/material-outlined/30/telegram-app.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/viber.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/twitter-circled--v1.png'>",
      "<img src='https://img.icons8.com/material-outlined/30/snapchat.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/vk-circled.png'>",
      "<img src='https://img.icons8.com/material-outlined/30/instagram-new--v1.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/facebook-new.png'>",
      "<img src='https://img.icons8.com/ios-filled/30/tiktok--v1.png'>",
      "<img src='https://img.icons8.com/material-outlined/30/telegram-app.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/viber.png'>",
      "<img src='https://img.icons8.com/ios-glyphs/30/twitter-circled--v1.png'>",
      "<img src='https://img.icons8.com/material-outlined/30/snapchat.png'>"]
      for (let i=0; i<=15; i++) {
        document.getElementsByClassName('app__wrapper__card')[i].classList.remove('app__wrapper__card_isFlipped')
        document.getElementsByClassName('app__wrapper__card__face_back')[i].classList.remove('app__wrapper__card__face_back_active')
        let rnd = Math.floor(Math.random() * (mass.length - 1)); 
        document.getElementsByClassName('app__wrapper__card__face_back')[i].innerHTML = mass[rnd]
        mass.splice(rnd, 1)
      }
      document.getElementsByClassName('app__level')[0].classList.toggle('app__level_close')
      this.attempts = document.querySelector('input[name="level"]:checked').value
    }
  }
}
</script>

<style scoped lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');

  .app {
    background-color: #eeeeee;

    &__header {
      text-align: center;
      color: grey;
      font-size: 30px;
      margin-bottom: 20px;
      font-family: 'Roboto', sans-serif;
    }

    &__panel {
      justify-content: center;
      display: flex;

      &__attempts {
        font-family: 'Roboto', sans-serif;
        font-size: 20px;
        color: red;
        margin-right: 385px;
      }

      &__repeat {
        cursor: pointer;
        width: 15px;
        height: 15px;
        margin-top: 5px;
      }
    }

    &__wrapper {
      display: grid;
      grid-template-columns: 120px 120px 120px 100px;
      background: linear-gradient(160deg, #26c6da, 50%, #ab47bc);
      padding: 25px;
      width: fit-content;
      margin: 10px auto;
      border-radius: 10px;
      box-shadow: 10px 10px 10px rgba(0,0,0,0.5);

      &__card {
        width: 100px;
        height: 100px;
        transition: transform 1s;
        transition: 1s;
        transform-style: preserve-3d;
        cursor: pointer;
        user-select: none;
        margin-top: 20px;

        &:nth-child(1), &:nth-child(2), &:nth-child(3), &:nth-child(4) {
          margin-top: 0;
        }

        &_isFlipped {
          transform: rotateY(180deg);
          pointer-events: none;
        }

        &__face {
          position: absolute;
          width: 100%;
          height: 100%;
          line-height: 100px;
          color: white;
          text-align: center;
          font-size: 40px;
          border-radius: 10px;
          backface-visibility: hidden;

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
        height: 200px;
        border-radius: 30px;
        padding: 20px;
        margin-top: 200px;

        &__header {
          font-family: 'Roboto', sans-serif;
          margin-bottom: 20px;
        }

        &__lvlBlock {
          margin-bottom: 10px;
          margin-left: 15px;

          &__radio {
            cursor: pointer;
            width: 20px;
          }

          &__label {
            font-family: 'Roboto', sans-serif;
            cursor: pointer;
            color: #424242;
          }

          &__btn {
            font-family: 'Roboto', sans-serif;
            cursor: pointer;
            border: 1px solid #00A1F1;
            text-align: center;
            color: #00A1F1;
            margin-top: 23px;
            transition: 1s;

            &:hover {
              color: white;
              background: #00A1F1;
            }
          }
        }
      }
    }
  }
</style>