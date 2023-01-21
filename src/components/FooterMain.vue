<template>
  <div class="footer-main">
    <a href="https://instagram.com/3points_kz?igshid=OGQ2MjdiOTE=" target="_blank" class="footer-main__link">
      <img src="../assets/insta4.png" alt="instagram" class="footer-main__link-img">
    </a>
  </div>
</template>
<script>
export default {
  name: 'FooterMain'

}
</script>

<style>
.footer-main {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 0 20px;
  background-color: #f5f5f5;
  height: 80px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-color: black;
}

.data {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  align-items: center;
  height: 100%;
}

.footer-main img {
  width: 75px;
  height: 75px;
}

.copyrights {
  font-size: 12px;
  color: rgb(255, 255, 255);
}

.creator {
  font-size: 12px;
  color: rgb(0, 0, 0);
  position: fixed;
  bottom: 0;
  right: 0;
}

@media screen and (min-width: 768px) {
  .footer-main {
    height: 150px;
  }

  .footer-main img {
    width: 145px;
    height: 145px;
  }

  .creator {
    font-size: 20px;
  }

}
</style>
