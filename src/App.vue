<script setup>
import Appwheel from '@/components/Appwheel.vue'
import AppModal from './components/AppModal.vue'
import { ref } from 'vue'

const title = ref('Поздравляем!')
const subtitle = ref('Вы выиграли еще одно вращение колеса!')
const btn = ref('Крутить снова!')
const isModalVisible = ref(false)
const childClass = ref('waiting')
const isButtonDisabled = ref(false)

const isFirstTry = ref(true)

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
  }, 4000)
}

function submit() {
  console.log('submit')
}
</script>

<template>
  <section class="main">
    <img class="main__hidden" src="/bg/background.png" alt="background" />
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
        <img class="main__bg" src="@/assets/Art.png" alt="art" />
      </div>
    </div>
    <AppModal class="main__modal" v-if="isModalVisible">
      <h2 class="main__title">{{ title }}</h2>
      <p class="main__text">{{ subtitle }}</p>
      <button class="main__button" @click="isFirstTry ? reroll() : submit()">{{ btn }}</button>
    </AppModal>
  </section>
</template>

<style lang="scss">
@import '@/assets/scss/reset.scss';

.main {
  position: relative;
  background-image: url('/bg/background.png');
  background-repeat: no-repeat;
  background-size: 100%;
  padding-top: 32px;
  &__hidden {
    height: 1px;
  }
  &__logo {
    display: flex;
    align-items: center;
    justify-content: center;
    img {
      width: 10vw;
    }
  }
  &__wheel {
    position: absolute;
    left: 50%;
    top: -40px;
    transform: translate(-50%, 0);
    z-index: 1;
  }
  &__mock {
    width: 100%;
  }
  &__bg {
    width: 100%;
    position: absolute;
    left: 0%;
    top: 10%;
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

@media screen and (max-width: 480px) {
  .main {
  }
}
</style>
