<template>
  <div class="navbar">
    <h1>3points store</h1>
    <div class="creator">
      <p>@_krivalex_</p>
    </div>
  </div>
</template>
<script>
export default {
  name: 'NavbarMain'

}
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 0 20px;
  background-color: #f5f5f5;
  height: 100px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-color: black;

}

.navbar h1 {
  font-size: 2rem;
  font-weight: 700;
  color: #ffffff;
  font-family: "Sacramento", sans-serif;
}

.name {
  width: 320px;
  height: 100px;
}

.logo {
  width: 60px;
  height: 60px;
  border-radius: 50%;
}

.neonText {
  color: #fff;
  text-shadow:
    0 0 7px #fff,
    0 0 10px #fff,
    0 0 21px #fff,
    0 0 42px #bc13fe,
    0 0 82px #bc13fe,
    0 0 92px #bc13fe,
    0 0 102px #bc13fe,
    0 0 151px #bc13fe;
}


h1,
h2 {
  text-align: center;
  font-weight: 400;
}

h1 {
  font-size: 6.2rem;
  animation: pulsate 1.5s infinite alternate;
  border: 0.2rem solid #fff;
  border-radius: 2rem;
  padding: 0.4em;
  box-shadow: 0 0 .2rem #fff,
    0 0 .2rem #fff,
    0 0 2rem #bc13fe,
    0 0 0.8rem #bc13fe,
    0 0 2.8rem #bc13fe,
    inset 0 0 1.3rem #bc13fe;
}

@keyframes pulsate {

  100% {

    text-shadow:
      0 0 4px #fff,
      0 0 11px #fff,
      0 0 19px #fff,
      0 0 40px #bc13fe,
      0 0 80px #bc13fe,
      0 0 90px #bc13fe,
      0 0 100px #bc13fe,
      0 0 150px #bc13fe;

  }

  0% {

    text-shadow:
      0 0 2px #fff,
      0 0 4px #fff,
      0 0 6px #fff,
      0 0 10px #bc13fe,
      0 0 45px #bc13fe,
      0 0 55px #bc13fe,
      0 0 70px #bc13fe,
      0 0 80px #bc13fe;

  }
}
</style>
