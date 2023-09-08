<script setup>
import Appwheel from '@/components/Appwheel.vue'
import AppModal from '@/components/AppModal.vue'
import AppFooter from '@/components/AppFooter.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue'

const title = ref('Поздравляем!')
const subtitle = ref('Вы выиграли еще одно вращение колеса!')
const btn = ref('Крутить снова!')
const isModalVisible = ref(false)
const childClass = ref('waiting')
const isButtonDisabled = ref(false)

const isFirstTry = ref(true)

const screenWidth = ref(window.innerWidth)
const screenHeight = ref(window.innerHeight)

// Обновление размеров при изменении размеров окна
const updateScreenSize = () => {
  screenWidth.value = window.innerWidth
  screenHeight.value = window.innerHeight
}

// Добавляем слушатель при монтировании компонента
onMounted(() => {
  window.addEventListener('resize', updateScreenSize)
})

// Удаляем слушатель при размонтировании компонента
onBeforeUnmount(() => {
  window.removeEventListener('resize', updateScreenSize)
})

function firstSpin() {
  childClass.value = 'spin'
  isButtonDisabled.value = true
}
function firstSpinDone() {
  isModalVisible.value = true
  isButtonDisabled.value = false
}

function reroll() {
  isModalVisible.value = false
  childClass.value = 'secondSpin'
  setTimeout(() => {
    isFirstTry.value = false
    subtitle.value = 'Вы получаете 500 монет за выполнение заданий и еженедельный кэшбек 10%!'
    btn.value = 'Забрать'
    isModalVisible.value = true
  }, 4500)
}

function submit() {
  window.location.href = 'https://drgnreturn.com/'
}
</script>

<template>
  <section class="main">
    <div class="main__mock">
      <div class="main__logo">
        <img src="./assets/logo.png" alt="dragonmoney" />
      </div>
      <div>
        <Appwheel
          class="main__wheel"
          :wellClass="childClass"
          :isButtonDisabled="isButtonDisabled"
          @firstSpin="firstSpin"
          @firstSpinDone="firstSpinDone"
        />

        <img v-if="screenWidth > 330" class="main__bg" src="@/assets/Art.png" alt="art" />
        <img v-else class="main__bg" src="@/assets/Art__mobile.png" alt="art" />
      </div>
    </div>
    <AppModal class="main__modal" v-if="isModalVisible">
      <h2 class="main__title">{{ title }}</h2>
      <p class="main__text">{{ subtitle }}</p>
      <button class="main__button" @click="isFirstTry ? reroll() : submit()">{{ btn }}</button>
    </AppModal>
  </section>
  <AppFooter />
</template>

<style lang="scss">
@import '@/assets/scss/reset.scss';
#app {
  overflow: hidden;
}
section,
header,
footer {
  padding: 0 15px;
}

@media (min-width: 575.98px) {
  section,
  header,
  footer {
    padding: 0 calc(50vw - 270px);
  }
}

@media (min-width: 767.98px) {
  section,
  header,
  footer {
    padding: 0 calc(50vw - 360px);
  }
}

@media (min-width: 991.98px) {
  section,
  header,
  footer {
    padding: 0 calc(50vw - 480px);
  }
}

@media (min-width: 1199.98px) {
  section,
  header,
  footer {
    padding: 0 calc(50vw - 590px);
  }
}
.main {
  position: relative;
  background-image: url('/bg/background.png');
  background-repeat: no-repeat;
  background-position: center top;
  padding-top: 32px;
  padding-bottom: 150px;

  &__hidden {
    height: 1px;
  }
  &__logo {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 17%;
    img {
      width: 192px;
      z-index: 1;
      // width: 10vw;
    }
  }
  &__wheel {
    position: absolute;
    left: 50%;
    top: -40px;
    transform: translate(-50%, 0);
    z-index: 1;
  }
  &__bg {
    min-width: 100%;
    position: absolute;
    left: 50%;
    top: 10%;
    transform: translate(-50%);
  }
  &__title {
    color: #181a25;
    font-family: 'Exo 2';
    font-size: 72px;
    font-weight: 700;
  }
  &__text {
    color: #181a25;
    text-align: center;
    font-family: 'Exo 2';
    font-size: 36px;
    font-weight: 500;
    margin: 24px 0 64px;
    max-width: 700px;
  }
  &__button {
    border-radius: 8px;
    padding: 19px 0;
    background: #181a25;
    color: #fff;
    font-family: 'Exo 2';
    font-size: 32px;
    font-weight: 900;
    text-transform: uppercase;
    min-width: 360px;
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
      box-shadow: 0px 0px 6px 4px rgba(255, 255, 255, 0.51);
    }
  }
}

@media screen and (max-width: 992px) {
  .main {
    &__title {
      font-size: calc(15px + 56 * (100vw / 1920));
    }
    &__text {
      font-size: calc(10px + 26 * (100vw / 1920));
    }
    &__button {
      font-size: calc(13px + 19 * (100vw / 1920));
    }
  }
}
@media screen and (max-width: 768px) {
  .main {
    background-position: center bottom;

    &__bg {
      min-width: auto;
      width: 235%;
    }
  }
}
@media screen and (max-width: 576px) {
  .main {
    &__text {
      margin: 10px 0 25px;
    }
  }
}
@media screen and (max-width: 480px) {
  .main {
    background-image: url('/bg/background.png');
    
    &__logo {
      margin-bottom: 95px;
      img {
        width: 108px;
      }
    }
    &__button {
      min-width: auto;
      width: 100%;
      padding: 8px 0;
    }
    &__bg{
      top: 15%;
    }
    &__wheel {
      top: -20px;
    }
  }
}
@media screen and (max-width: 330px){
  .main{
    &__bg {
      top: 16%;
      width: auto ;
    }
  }
}
</style>
