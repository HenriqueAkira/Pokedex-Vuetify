<template>
  <div >
    <div class="intro-img"></div>
    <div class="intro-text">
      <h1>Teste</h1>
      <p>teste</p>
    </div>
  </div>
  
</template>

<script>
export default {

}
</script>

<style>

.intro-img{
  height: 45em;
  background-image: url("@/assets/background.gif");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  filter: blur(4px);
}

.intro-text {
  background-color: rgb(255, 255, 255); 
  background-color: rgb(255, 255, 255);
  color: rgb(219, 79, 79);
  font-weight: bold;
  border: 3px solid #f1f1f1;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
  width: 80%;
  padding: 20px;
  text-align: center;
}



</style>