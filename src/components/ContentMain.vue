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
          <div class="quest_box">
            <label for="leg">Введите длину стопы</label>
            <button class="open-model-button" @click="openModel">
              <img class="question" src="../assets/question.png" alt="question">
            </button>
            <div class="modal-open-sex">
              <ModalDialog v-show="model" @hide-model="hideModal">
                <img class="foot-intersection" src="../assets/foot.jpg" alt="foot-intersection">
                <h2>Как измерить длину стопы?</h2>
                <p>1. Стоя на прямой ноге, на полу, на бумаге нарисуйте линию от кончика пальца до кончика пальца.</p>
                <p>2. Поставьте стопу на линию и нарисуйте линию от кончика пальца до кончика пальца.</p>
                <p>3. Измерьте расстояние между линиями.</p>
                <p>4. Введите полученное значение в поле ввода.</p>
              </ModalDialog>
            </div>


          </div>
          <input :value="foot" @input="inputFoot" class="input" type="text" placeholder="Длина ноги в сантиметрах">
        </form>
      </div>
    </div>

    <div class="radios">

      <div class="gender">
        <h2 for="man">Пол: </h2>
        <form>
          <div>
            <input :value="man" @input="inputMan" class="radio-button" type="radio" name="gender">
            <label for="man">Мужской</label>
          </div>

          <div>
            <input :value="woman" @input="inputWoman" class="radio-button" type="radio" name="gender">
            <label for="woman">Женский</label>
          </div>
        </form>
      </div>

      <div class="ortopedic">
        <h2 for="man">Ортопедическая?</h2>
        <input :value="ortopedic" @input="inputOrtopedic" class="radio-button" type="checkbox" name="ortopedic">
      </div>



    </div>

    <div class="color">
      <h2 for="color-choice">Какие цвета?</h2>
      <div class="color-choice">
        <div class="one-color">
          <label id="red">Красный</label>
          <input :value="colors" @input="inputRED" class="radio-button" type="checkbox" name="red">
        </div>
        <div class="one-color">
          <label id="black">Черный</label>
          <input :value="colors" @input="inputBLACK" class="radio-button" type="checkbox" name="black">
        </div>
        <div class="one-color">
          <label id="white">Белый</label>
          <input :value="colors" @input="inputWHITE" class="radio-button" type="checkbox" name="white">
        </div>
        <div class="one-color">
          <label id="grey">Серый</label>
          <input :value="colors" @input="inputGREY" class="radio-button" type="checkbox" name="grey">
        </div>
        <div class="one-color">
          <label id="green">Зеленый</label>
          <input :value="colors" @input="inputGREEN" class="radio-button" type="checkbox" name="green">
        </div>
        <div class="one-color">
          <label id="rainbow">Нестандартный</label>
          <input :value="colors" @input="inputSTRANGE" class="radio-button" type="checkbox" name="rainbow">
        </div>
      </div>
    </div>

    <div class="calc-button">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <button class="button_calc" type="submit" @click="calculate">Рассчитать</button>
    </div>

    <div v-if="this.ru_result > 0" class="result" id="result">

      <h2>Ваш размер обуви: <strong>{{ this.ru_result }}</strong></h2>
      <ul>
        <li>По американской системе: {{ this.usa_result }}</li>
        <li>По европейской системе: {{ this.eu_result }}</li>
        <li>По российской системе: {{ this.ru_result }}</li>
      </ul>


      <div class="many-cards">
        <ManyCard :size_eu="Number(this.eu_result)" :colors="this.colors" />
      </div>


    </div>
    <div v-else-if='this.height === ""' class="result">
      <h4>Подсказка:</h4>
      <h2>Укажите ваш рост📏</h2>
    </div>
    <div v-else-if='isNaN(this.foot) || this.foot === ""' class="result">
      <h4>Подсказка:</h4>
      <h2>Укажите размер вашей ноги🦶</h2>
    </div>
    <div v-else-if="this.man === false && this.woman === false" class="result">
      <h4>Подсказка:</h4>
      <h2>Укажите ваш пол <br /> 👨/👩</h2>
    </div>
    <div v-else-if="this.colors.length === 0" class="result">
      <h4>Подсказка:</h4>
      <h2>Выберите цвет обуви🌈</h2>
    </div>
    <div v-else-if="this.ru_result === undefined" class="result">
      <h2>Похоже, что вы не вписываетесь в стандартные размеры обуви 🤔</h2>
    </div>

    <div v-else class="result no-validation">
      <h4>Подсказка:</h4>
      <h2>Нажмите на кнопку <b>"Рассчитать"</b>⚙️</h2>
    </div>





  </div>
</template>
<script>
import ManyCard from './ManyCard.vue'
import ModalDialog from '@/components/UI/ModalDialog.vue'



const foot_size_sm_woman = [22.8, 23.1, 23.5, 23.8, 24.1, 24.5, 24.8, 25.1, 25.4, 25.7, 26.0, 26.7, 27.6]
const foot_size_sm_man = [24.1, 24.4, 24.8, 25.4, 25.7, 26, 26.7, 27.0, 27.3, 27.9, 28.3, 28.6, 29, 29.4, 30]

const foot_size_USA_woman = [5, 5.5, 6, 6.5, 7, 7.5, 8, 8.5, 9, 9.5, 10, 10.5, 11]
const foot_size_USA_man = [6.5, 7, 7.5, 8, 8.5, 9, 9.5, 10, 10.5, 11, 11.5, 12, 12.5, 13, 13.5]

const foot_size_RU_woman = [35, 35.5, 35 - 36, 36, 36.5, 37, 37.5, 38, 38.5, 39, 39.5, 40, 40.5, 41, 41.5]
const foot_size_RU_man = [37.5, 38, 39, 39.5, 40, 41, 41.5, 42, 43, 43.5, 44, 44.5, 45, 46, 47]

const foot_size_EU_woman = [35, 35.5, 36, 37, 37.5, 38, 38.5, 39, 40, 40.5, 41, 42, 42.2]
const foot_size_EU_man = [38.5, 39, 40, 40.5, 41, 42, 42.5, 43, 44, 44.5, 45, 46, 46.5, 47, 48]


export default {
  data() {
    return {
      height: "",
      foot: "",
      man: false,
      woman: false,
      ortopedic: false,
      ru_result: 0,
      eu_result: 0,
      usa_result: 0,
      colors: [],
      model: false,
    }
  },
  name: 'ContentMain',
  components: { ManyCard, ModalDialog },
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
    },
    inputRED() {
      if (this.colors.includes("red")) {
        this.colors = this.colors.filter(cur => cur !== "red")
      } else {
        this.colors.push("red")
      }
    },
    inputBLACK() {
      if (this.colors.includes("black")) {
        this.colors = this.colors.filter(cur => cur !== "black")
      } else {
        this.colors.push("black")
      }
    },
    inputWHITE() {
      if (this.colors.includes("white")) {
        this.colors = this.colors.filter(cur => cur !== "white")
      } else {
        this.colors.push("white")
      }
    },
    inputGREY() {
      if (this.colors.includes("grey" || "gray" || "silver")) {
        this.colors = this.colors.filter(cur => cur !== "grey" && cur !== "gray" && cur !== "silver")
      } else {
        this.colors.push("grey", "gray", "silver")
      }
    },
    inputGREEN() {
      if (this.colors.includes("green")) {
        this.colors = this.colors.filter(cur => cur !== "green")
      } else {
        this.colors.push("green")
      }
    },
    inputSTRANGE() {
      if (this.colors.includes("light_green" && "Cactus Jack" && "camouflage")) {
        this.colors = this.colors.filter(cur => cur !== "light_green" && cur !== "Cactus Jack" && cur !== "camouflage")
      } else {
        this.colors.push("light_green", "Cactus Jack", "camouflage")
      }
    },
    openModel() {
      console.log("писька")
      this.model = true
    },
    hideModal() {
      this.model = false
    }
  }
}
</script>

<style scoped>
.result {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  font-size: 20px;
  margin-top: 15px;
  margin-bottom: 40px;
  padding: 0 15px;
  text-align: center;
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

.input-group form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
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
  margin-bottom: 10px;
}

.gender h2 {
  margin-right: 10px;
}

.gender form {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.gender form div {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.gender form label {
  margin-right: 10px;
  font-size: 25px;
}

.gender form input {
  margin: 5px;
  margin-left: 15px;
  margin-right: 10px;
  transform: scale(2.0);
  opacity: 0.9;
  cursor: pointer;
}

.ortopedic {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
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

.button_calc {
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

.button_calc::before {
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

.button_calc:hover,
.button_calc:focus {
  color: #313133;
  transform: translateY(-6px);
}

.button_calc:hover::before,
.button_calc:focus::before {
  opacity: 1;
}

.button_calc::after {
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

.button_calc:hover::after,
.button_calc:focus::after {
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

.color {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.color h2 {
  margin-bottom: 20px;
}

.color input {
  margin: 5px;
  margin-left: 15px;
  margin-right: 7px;
  transform: scale(2.0);
  opacity: 0.9;
  cursor: pointer;
}

.color label {
  font-size: 20px;
  text-align: center;
}

#red {
  -webkit-text-stroke-color: red;
  -webkit-text-stroke-width: 0.5px;
  color: white;
}

#grey {
  -webkit-text-stroke-color: rgb(41, 41, 41);
  color: gray;
  -webkit-text-stroke-width: 0.5px;
}

#green {
  -webkit-text-stroke-color: rgb(15, 202, 15);
  -webkit-text-stroke-width: 0.5px;
  color: white;
}

#white {
  -webkit-text-stroke-color: rgb(0, 0, 0);
  color: white;
  -webkit-text-stroke-width: 0.5px;
}

#black {
  -webkit-text-stroke-color: black;
  color: black;
  -webkit-text-stroke-width: 1px;
}

#rainbow {
  background: linear-gradient(90deg, rgba(255, 0, 0, 1) 0%, rgb(255, 179, 0) 17%, rgb(246, 255, 0) 34%, rgb(30, 255, 0) 51%, rgb(5, 198, 219) 68%, rgb(34, 0, 255) 85%, rgb(255, 0, 255) 100%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  -webkit-text-stroke-color: black;
  -webkit-text-stroke-width: 0.5px;
}

.color-choice {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.one-color {
  display: flex;
  justify-content: center;
  flex-direction: column-reverse;
  align-items: center;
  margin-right: 13px;
  margin-bottom: 5px;
}

.question {
  max-width: 30px;
  max-height: 30px;
}

.quest_box {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.quest_box label {
  font-size: 30px;
  margin-right: 10px;
}

.modal-open-sex {
  z-index: 100;
}

.no-validation {
  height: 100px;
}

.foot-intersection {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.open-model-button {
  border-radius: 50%;
  height: 30px;
  width: 30px;
}
</style>
