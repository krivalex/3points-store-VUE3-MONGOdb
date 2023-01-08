<template>
  <div class="content-main">
    <div class="img-beaty">
      <img src="../assets/head.png" alt="logo">
    </div>
    <div class="input-group">

      <div class="height">
        <form @submit.prevent>
          <label for="height">Введите свой рост</label>
          <input :value="height" @input="inputHeight" class="input" type="text" placeholder="Ваш рост">
        </form>
      </div>

      <div class="leg">
        <form @submit.prevent>
          <label for="leg">Введите длину ноги</label>
          <input :value="foot" @input="inputFoot" class="input" type="text" placeholder="Длина ноги в сантиметрах">
        </form>
      </div>
    </div>

    <div class="radios">

      <div class="gender">
        <h2 for="man">Пол: </h2>
        <form>
          <input :value="man" @input="inputMan" class="radio-button" type="radio" name="gender">
          <label for="man">Мужской</label>

          <input :value="woman" @input="inputWoman" class="radio-button" type="radio" name="gender">
          <label for="woman">Женский</label>
        </form>
      </div>

      <div class="ortopedic">
        <h2 for="man">Ортопедическая?</h2>
        <input :value="ortopedic" @input="inputOrtopedic" class="radio-button" type="checkbox" name="ortopedic">
      </div>

    </div>

    <div class="calc-button">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <button class="button" type="submit" @click="calculate">Рассчитать</button>
    </div>

    <div v-if="this.ru_result > 0" class="result" id="result">

      <h2>Ваш размер обуви: <strong>{{ this.ru_result }}</strong></h2>
      <ul>
        <li>По американской системе: {{ this.usa_result }}</li>
        <li>По европейской системе: {{ this.eu_result }}</li>
        <li>По российской системе: {{ this.ru_result }}</li>
      </ul>


      <div class="many-cards">
        <ManyCard />
      </div>


    </div>
    <div v-else-if="this.height === 0" class="result">
      <h2>Укажите ваш рост📏</h2>
    </div>
    <div v-else-if="isNaN(this.foot) || this.foot === 0" class="result">
      <h2>Укажите размер вашей ноги🦶</h2>
    </div>
    <div v-else-if="this.man === false && this.woman === false" class="result">
      <h2>Укажите ваш пол 👨/👩</h2>
    </div>
    <div v-else-if="this.ru_result === undefined" class="result">
      <h2>Похоже, что вы не вписываетесь в стандартные размеры обуви 🤔</h2>
    </div>





  </div>
</template>
<script>
import ManyCard from './ManyCard.vue'



const foot_size_sm_woman = [22.8, 23.1, 23.5, 23.8, 24.1, 24.5, 24.8, 25.1, 25.4, 25.7, 26.0, 26.7, 27.6]
const foot_size_sm_man = [24.1, 24.4, 24.8, 25.4, 25.7, 26, 26.7, 27.0, 27.3, 27.9, 28.3, 28.6, 29, 29.4, 30]

const foot_size_USA_woman = [5, 5.5, 6, 6.5, 7, 7.5, 8, 8.5, 9, 9.5, 10, 10.5, 11]
const foot_size_USA_man = [6.5, 7, 7.5, 8, 8.5, 9, 9.5, 10, 10.5, 11, 11.5, 12, 12.5, 13, 13.5]

const foot_size_RU_woman = [35, 35.5, 35 - 36, 36, 36.5, 37, 37.5, 38, 38.5, 39, 39.5, 40, 40.5, 41, 41.5]
const foot_size_RU_man = [37.5, 38, 39, 39.5, 40, 41, 41.5, 42, 43, 43.5, 44, 44.5, 45, 46, 47]

const foot_size_EU_woman = [35, 35.5, "36(3)", 37, "37.5(4.5)", 38, "38.5(5.5)", "39(6)", "40(6.5)", "40.5(7)", "41(7.5)", "42(8.5)", 42.2]
const foot_size_EU_man = [38.5, 39, 40, 40.5, 41, 42, 42.5, 43, 44, 44.5, 45, 46, 46.5, 47, 48]


export default {
  data() {
    return {
      height: 0,
      foot: 0,
      man: false,
      woman: false,
      ortopedic: false,
      ru_result: 0,
      eu_result: 0,
      usa_result: 0,
      update: false
    }
  },
  name: 'ContentMain',
  components: { ManyCard },
  methods: {
    calculate() {
      let foot = this.foot
      if (typeof this.foot === "string") {
        foot = this.foot.replace(",", ".")
      }

      if (this.woman) {
        let foot_value = foot < 0 ? foot_size_sm_woman.filter(cur => cur <= foot)[0] : foot_size_sm_woman.filter(cur => cur >= foot)[0];
        console.log(foot_value)
        this.ru_result = foot_size_RU_woman[foot_size_sm_woman.indexOf(foot_value)]
        this.eu_result = foot_size_EU_woman[foot_size_sm_woman.indexOf(foot_value)]
        this.usa_result = foot_size_USA_woman[foot_size_sm_woman.indexOf(foot_value)]
        this.foot = foot
        if (this.ortopedic) {
          this.ru_result += 0.5
          this.usa_result += 0.5
        }
      }
      if (this.man) {
        let foot_value = foot < 0 ? foot_size_sm_man.filter(cur => cur <= foot)[0] : foot_size_sm_man.filter(cur => cur >= foot)[0];
        console.log(foot_value)
        this.ru_result = foot_size_RU_man[foot_size_sm_man.indexOf(foot_value)]
        this.eu_result = foot_size_EU_man[foot_size_sm_man.indexOf(foot_value)]
        this.usa_result = foot_size_USA_man[foot_size_sm_man.indexOf(foot_value)]
        this.foot = foot
        if (this.ortopedic) {
          this.ru_result += 0.5
          this.usa_result += 0.5
        }
      }





    },
    inputHeight(event) {
      this.height = event.target.value
    },
    inputFoot(event) {
      this.foot = event.target.value
    },
    inputMan() {
      this.man = true
      this.woman = false
    },
    inputWoman() {
      this.man = false
      this.woman = true
    },
    inputOrtopedic() {
      if (this.ortopedic) {
        this.ortopedic = false
      } else {
        this.ortopedic = true
      }
    }
  }
}
</script>

<style>
.result {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  font-size: 20px;
  margin-top: 15px;
  margin-bottom: 40px;
}

.result strong {
  color: #ff0000;
  font-size: 40px;
}

#result {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  font-size: 20px;
  margin-top: 15px;
  margin-bottom: 40px;
}

.content-main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #f5f5f5;
}

.content-main h1 {
  font-size: 40px;
  margin-bottom: 20px;
  text-align: center;
}

.input-group {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 20px;
  font-size: 30px;
  margin-bottom: 50px;
}

.input-group input {
  width: 100%;
  height: 30px;
  border: 4px solid #ccc;
  border-color: linear-gradient(45deg, #fb0094, #0000ff, #00ff00, #ffff00, #ff0000, #fb0094, #0000ff, #00ff00, #ffff00, #ff0000);
  border-radius: 4px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}


.height {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.leg {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.input {
  width: 100%;
  height: 30px;
  border: 4px solid #ccc;
  border-radius: 4px;
  padding: 12px 20px;
  margin: 4px 0;
  box-sizing: border-box;
}

.input:focus {
  border-color: #0460ac;
  box-shadow: 0 0 10px #0b80e0;
  transition: box-shadow linear 1s
}

.input label {
  font-size: 25px;

}

.radios {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50vw;
  margin: 20px;
}

.gender {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.gender h2 {
  margin-right: 10px;
}

.gender form {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.gender form label {
  margin-right: 15px;
  font-size: 25px;
}

.gender form input {
  margin: 5px;
  margin-left: 15px;
  margin-right: 7px;
  transform: scale(2.0);
  opacity: 0.9;
  cursor: pointer;
}

.ortopedic {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.ortopedic input {
  margin-left: 20px;
  margin-top: 5px;
  transform: scale(2.0);
  opacity: 0.9;
  cursor: pointer;
}

.img-beaty {
  position: relative;
}

.heading {
  position: absolute;
  top: 90px;
}

.button {
  min-width: 300px;
  min-height: 60px;
  font-family: 'Nunito', sans-serif;
  font-size: 22px;
  text-transform: uppercase;
  letter-spacing: 1.3px;
  font-weight: 700;
  color: #313133;
  background: #4FD1C5;
  background: linear-gradient(90deg, rgba(129, 230, 217, 1) 0%, rgba(79, 209, 197, 1) 100%);
  border: none;
  border-radius: 1000px;
  box-shadow: 12px 12px 24px rgba(79, 209, 197, .64);
  transition: all 0.3s ease-in-out 0s;
  cursor: pointer;
  outline: none;
  position: relative;
  padding: 10px;
  margin-top: 15px;
}

button::before {
  content: '';
  border-radius: 1000px;
  min-width: calc(300px + 12px);
  min-height: calc(60px + 12px);
  border: 6px solid #00FFCB;
  box-shadow: 0 0 60px rgba(0, 255, 203, .64);
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  opacity: 0;
  transition: all .3s ease-in-out 0s;
}

.button:hover,
.button:focus {
  color: #313133;
  transform: translateY(-6px);
}

button:hover::before,
button:focus::before {
  opacity: 1;
}

button::after {
  content: '';
  width: 30px;
  height: 30px;
  border-radius: 100%;
  border: 6px solid #00FFCB;
  position: absolute;
  z-index: 1;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation: ring 1.5s infinite;
}

button:hover::after,
button:focus::after {
  animation: none;
  display: none;
}

@keyframes ring {
  0% {
    width: 30px;
    height: 30px;
    opacity: 0.8;
  }

  100% {
    width: 120px;
    height: 120px;
    opacity: 0;
  }
}
</style>
