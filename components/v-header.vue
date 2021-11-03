<template>
  <header>
    <div class="container">
      <div class="logo">
        <img src="~/assets/img/logo.png" alt="logo" />
      </div>
    </div>
  </header>
</template>

<script>
export default {}
</script>

<style lang="scss">
header {
  width: 100%;
  display: flex;

  .container {
    width: 100%;
    margin: 0 auto;
    max-width: 1260px;
    display: flex;
    align-items: center;
    justify-content: flex-start;

    .logo {
      padding-left: 120px;

      img {
        width: 120px;
        height: auto;
        padding: 32px 0;
      }
    }
  }
}

@media screen and (max-width: 767px) {
  header {
    .container {
      justify-content: center;
      .logo {
        padding-left: 0;
      }
    }
  }
}
</style>
