<template>
  <div class="content-main">
    <img src="../assets/head.png" alt="logo">
    <h1 class="heading">Калькулятор размера обуви</h1>
    <div class="input-group">

      <div class="height">
        <form>
          <label for="height">Введите свой рост</label>
          <input :value="height" @input="inputHeight" class="input" type="text" placeholder="Ваш рост">
        </form>
      </div>

      <div class="leg">
        <form>
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

    <div v-if="this.result > 0" class="result">
      <h2>Ваш размер обуви: {{ this.result }}</h2>
    </div>

  </div>
</template>
<script>

const foot_size_sm = [21, 21.5, 22, 22.5, 23, 23.5, 24, 24.5, 25, 25.5, 26, 26.5, 27, 27.5, 28, 28.5, 29, 29.5, 30, 30.5, 31, 31.5, 32]
const foot_size_index = [33, 34, 34, 35, 36, 37, 37, 38, 39, 40, 40, 41, 42, 43, 44, 44, 45, 46, 46, 47, 47, 48, 48]

export default {
  data() {
    return {
      height: "",
      foot: "",
      man: false,
      woman: false,
      ortopedic: false,
      result: 0

    }
  },
  name: 'ContentMain',
  methods: {
    calculate() {
      let foot = parseFloat(this.foot)
      let foot_value = foot < 0 ? foot_size_sm.filter(cur => cur <= foot)[0] : foot_size_sm.filter(cur => cur >= foot)[0];
      this.result = foot_size_index[foot_size_sm.indexOf(foot_value)]

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
.content-main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
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
  border: 4px solid rgb(255, 149, 2);
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
  margin-left: 10px;
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

.heading {
  position: absolute;
  top: 230px;
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
