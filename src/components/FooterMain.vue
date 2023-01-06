<template>
  <div class="footer-main">
    <a href="https://instagram.com/3points_kz?igshid=OGQ2MjdiOTE=" target="_blank" class="footer-main__link">
      <img src="../assets/insta.png.webp" alt="instagram" class="footer-main__link-img">
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
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' version='1.1' xmlns:xlink='http://www.w3.org/1999/xlink' xmlns:svgjs='http://svgjs.com/svgjs' width='1080' height='100' preserveAspectRatio='none' viewBox='0 0 1080 100'%3e%3cg mask='url(%26quot%3b%23SvgjsMask1023%26quot%3b)' fill='none'%3e%3crect width='1080' height='100' x='0' y='0' fill='url(%23SvgjsLinearGradient1024)'%3e%3c/rect%3e%3cpath d='M0 0L317.16 0L0 362.9z' filter='url(%23SvgjsFilter1025)' fill='%232d409e'%3e%3c/path%3e%3cpath d='M0 100L317.16 100L0 -262.9z' filter='url(%23SvgjsFilter1025)' fill='%232d409e'%3e%3c/path%3e%3cpath d='M1080 100L762.8399999999999 100L1080 -262.9z' filter='url(%23SvgjsFilter1025)' fill='%232d409e'%3e%3c/path%3e%3cpath d='M1080 0L762.8399999999999 0L1080 362.9z' filter='url(%23SvgjsFilter1025)' fill='%232d409e'%3e%3c/path%3e%3c/g%3e%3cdefs%3e%3cmask id='SvgjsMask1023'%3e%3crect width='1080' height='100' fill='white'%3e%3c/rect%3e%3c/mask%3e%3clinearGradient x1='22.69%25' y1='-245%25' x2='77.31%25' y2='345%25' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1024'%3e%3cstop stop-color='%230e2a47' offset='0'%3e%3c/stop%3e%3cstop stop-color='%2300459e' offset='1'%3e%3c/stop%3e%3c/linearGradient%3e%3cfilter height='130%25' id='SvgjsFilter1025'%3e%3cfeGaussianBlur in='SourceAlpha' stdDeviation='5' result='TopLeftG'%3e%3c/feGaussianBlur%3e%3cfeOffset dx='-5' dy='-5' in='TopLeftG' result='TopLeftO'%3e%3c/feOffset%3e%3cfeComponentTransfer in='TopLeftO' result='TopLeftC'%3e%3cfeFuncA type='linear' slope='0.7'%3e%3c/feFuncA%3e%3c/feComponentTransfer%3e%3cfeGaussianBlur in='SourceAlpha' stdDeviation='5' result='TopRightG'%3e%3c/feGaussianBlur%3e%3cfeOffset dx='5' dy='-5' in='TopRightG' result='TopRightO'%3e%3c/feOffset%3e%3cfeComponentTransfer in='TopRightO' result='TopRightC'%3e%3cfeFuncA type='linear' slope='0.7'%3e%3c/feFuncA%3e%3c/feComponentTransfer%3e%3cfeGaussianBlur in='SourceAlpha' stdDeviation='5' result='BottomLeftG'%3e%3c/feGaussianBlur%3e%3cfeOffset dx='-5' dy='5' in='BottomLeftG' result='BottomLeftO'%3e%3c/feOffset%3e%3cfeComponentTransfer in='BottomLeftO' result='BottomLeftC'%3e%3cfeFuncA type='linear' slope='0.7'%3e%3c/feFuncA%3e%3c/feComponentTransfer%3e%3cfeGaussianBlur in='SourceAlpha' stdDeviation='5' result='BottomRightG'%3e%3c/feGaussianBlur%3e%3cfeOffset dx='5' dy='5' in='BottomRightG' result='BottomRightO'%3e%3c/feOffset%3e%3cfeComponentTransfer in='BottomRightO' result='BottomRightC'%3e%3cfeFuncA type='linear' slope='0.7'%3e%3c/feFuncA%3e%3c/feComponentTransfer%3e%3cfeMerge%3e%3cfeMergeNode in='TopLeftC'%3e%3c/feMergeNode%3e%3cfeMergeNode in='TopRightC'%3e%3c/feMergeNode%3e%3cfeMergeNode in='BottomLeftC'%3e%3c/feMergeNode%3e%3cfeMergeNode in='BottomRightC'%3e%3c/feMergeNode%3e%3cfeMergeNode in='SourceGraphic'%3e%3c/feMergeNode%3e%3c/feMerge%3e%3c/filter%3e%3c/defs%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.data {
  display: flex;
  justify-content: space-b;
  flex-direction: column;
  align-items: center;
  height: 100%;
}

.footer-main img {
  width: 100px;
  height: 100px;
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
</style>
