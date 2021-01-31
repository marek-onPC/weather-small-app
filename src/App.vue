<template>
  <div class="mdl-layout mdl-js-layout mdl-layout--fixed-header mdl-layout__header--scroll">
    <header class="mdl-layout__header mdl-layout__header--transparent">
      <div class="mdl-layout__header-row">
        <span class="mdl-layout-title">Weather small app</span>
        <div class="mdl-layout-spacer"></div>
        <nav class="mdl-navigation">
          <router-link class="mdl-button mdl-js-button mdl-js-ripple-effect" to="/">Weather</router-link>
          <router-link class="mdl-button mdl-js-button mdl-js-ripple-effect" to="/about">About app</router-link>
        </nav>
      </div>
    </header>
    <main class="mdl-layout__content">
      <transition name="fade" mode="out-in">
        <router-view/>
      </transition>
    </main>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;

  .mdl {
    &-layout {
      background-image: url('https://images.unsplash.com/photo-1534794048419-48e110dca88e?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1896&q=80');
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;

      &__header-row {
        background: linear-gradient(to bottom, rgba(#000, 1), rgba(#000, 0));
      }

      &-title {
        letter-spacing: 1.5px;
      }
    }

    &-button {
      color: #fff;
    }
  }
}

html {
  scrollbar-color: white black;

  .mdl-layout__content {
    scrollbar-width: thin;
  }

  ::-webkit-scrollbar {
    width: 5px;
  }

  ::-webkit-scrollbar-track {
    background: #000;
  }

  ::-webkit-scrollbar-thumb {
    background: #fff;
  }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter-from, .fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
