<template>
  <div id="app">
    <section class="slider">
        <div
        @mouseover="stopRotation()"
        @mouseout="startRotation()"
        class="slider__wrapper">
          <div class="slider__img">
            <img :src="currentImg" alt="abstract img">
          </div>
        <ul class="slider__controls">
          <li class="slider__controller slider__controller--arrow">
            <a @click="prev()" href="#">
              <span>
                <i class="fas fa-arrow-left"></i>
              </span>
            </a>
          </li>
          <li class="slider__controller">
            <a href="#">
              <span>
                Add a CLI to Node Apps with Vantage
              </span>
            </a>
          </li>
          <li class="slider__controller">
            <a href="#">
              <span>
                NewSprint, Spectacle
              </span>
            </a>
          </li>
          <li class="slider__controller">
            <a href="#">
              <span>
                Small Modules: Tales from a Serial Module Author
              </span>
            </a>
          </li>
          <li class="slider__controller">
            <a href="#">
              <span>
                The End
              </span>
            </a>
          </li>
          <li class="slider__controller slider__controller--arrow">
            <a @click="next()" href="#">
              <span>
                <i class="fas fa-arrow-right"></i>
              </span>
            </a>
          </li>
        </ul>
        </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      imgs: [
        'https://picsum.photos/700/300?image=1',
        'https://picsum.photos/700/300?image=2',
        'https://picsum.photos/700/300?image=3',
      ],

      currentIndex: 0,
      timer: null,
    }
  },

  methods: {
    startRotation() {
      this.timer = setInterval(this.next, 3000);
    },

    stopRotation() {
      clearInterval(this.timer);
      this.timer = null;
    },

    next() {
      this.currentIndex += 1;
    },

    prev() {
      this.currentIndex -= 1;
    }
  },

  computed: {
    currentImg() {
      return this.imgs[Math.abs(this.currentIndex) % this.imgs.length];
    }
  },

  mounted() {
    this.startRotation();
  }
};
</script>

<style lang="scss">
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
  padding: 0;
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.slider {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  height: 100vh;
  margin: auto;
  background-image: linear-gradient(to bottom right, #e559a6, #6cde5b);

  &__wrapper {
    width: 700px;
  }

  &__controls {
    display: flex;
    list-style: none;
    background-color: rgba(0,0,0,.2);
  }

  &__controller {
    flex: 2;
    display: flex;
    text-align: center;

    a {
      &,
      &:link,
      &:visited {
        flex-basis: 100%;
        text-decoration: none;
        color: #fff;
        display: flex;
        align-items: center;

        &:hover {
          background-color: rgba(0,0,0,.4);
        }
      }

      span {
        flex-basis: 100%;
      }
    }

    &--arrow {
      flex: 1;
      a {
        color: #fff;
      }
    }
  }
}

.fade-enter-active, .fade-leave-active {
 transition: all 0.8s ease;
 overflow: hidden;
 visibility: visible;
 opacity: 1;
 position: absolute;
}
.fade-enter, .fade-leave-to {
 opacity: 0;
 visibility: hidden;
}
</style>
