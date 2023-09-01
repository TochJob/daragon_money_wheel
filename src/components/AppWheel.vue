<script setup>
import AppArrow from '@/components/AppArrow.vue'
import { ref, defineEmits, defineProps } from 'vue'

const props = defineProps({
  wellClass: String,
  isButtonDisabled: Boolean
})
const emit = defineEmits('firstSpinDone')

const wheel = ref(null)

function spin() {
  emit('firstSpin')
  setTimeout(() => {
    emit('firstSpinDone')
  }, 4500)
}
</script>
<template>
  <div class="wheel">
    <AppArrow class="wheel__arrow" />
    <img
      class="wheel__wheel"
      :class="props.wellClass"
      ref="wheel"
      src="@/assets/wheel.png"
      alt="wheel"
    />
    <button @click="spin" :disabled="isButtonDisabled" class="wheel__button">КРУТИТЬ</button>
  </div>
</template>
<style lang="scss" scoped>
@import '@/assets/scss/animations.scss';
.wheel {
  display: inline-flex;
  position: relative;
  justify-content: center;
  &__wheel {
    width: 51%;
  }
  &__arrow {
    position: absolute;
    top: 8%;
    left: 50%;
    transform: translate(-50%, 0);
    z-index: 1;
  }
  &__button {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 50%;
    background: #f6f3f3;
    box-shadow:
      0px 14px 7px 0px #fff inset,
      0px -12px 12px 0px rgba(0, 0, 0, 0.25) inset;
    color: #fe8f16;
    text-shadow: 0px 4px 4px rgba(255, 255, 255, 0.25);
    font-family: 'Exo 2';
    font-size: calc(14px + 22 * (100vw / 1920));

    font-weight: 900;
    border: none;
    width: 12vw;
    height: 12vw;
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
      box-shadow:
        0px 14px 7px 0px #fff inset,
        0px -12px 12px 0px rgba(0, 0, 0, 0.25) inset,
        0px 0px 24px 0px rgba(0, 0, 0, 0.72);
    }
  }
  .waiting {
    animation: rest 3s infinite alternate;
  }
  .spin {
    animation: 4s firstSpin ease-out forwards;
  }
  .secondSpin {
    animation: 4s secondSpin ease-out forwards;
  }
}
@media screen and (max-width: 1200px) {
  .wheel {
    &__button {
      font-size: calc(14px + 9 * (100vw / 1920));
    }
    &__arrow{
      width: 50px;
    }
  }
}
@media screen and (max-width: 768px) {

}
</style>
