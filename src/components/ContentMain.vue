<template>
  <div class="content-main">
    <h1>Калькулятор размера обуви</h1>
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
        <h2 for="man">Ваш пол?</h2>
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
  height: 70vh;
  width: 100vw;
  background-color: #f5f5f5;
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
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}

.radios {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50vw;
  margin: 20px;
}
</style>
