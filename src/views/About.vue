<template>
  <div class="about">
    <h1 class="about__title">About</h1>
    <div class="about__inner">
      <p>This site has been built as a Single Page Application in Vue.js framework and Material Design Lite framework.</p>
      <p>All weather data comes from Open Weather API.</p>
      <p>Photos comes from unsplash.com</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.about {
  color: #fff;

  &__title {
    text-align: center;
    text-shadow: 1px 1px 2px #777;
  }

  &__inner {
    padding: 50px;
    background-color: rgba(0, 0, 0, 0.7);

    p {
      font-size: 18px;
      padding-bottom: 15px;
      margin-bottom: 25px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.3);
    }
  }
}
</style>
