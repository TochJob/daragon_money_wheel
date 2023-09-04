<script setup></script>
<template>
  <div class="modal">
    <div class="modal__box">
      <slot></slot>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.modal {
  position: fixed;
  background: #0000007e;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 3;
  display: flex;
  align-items: center;
  justify-content: center;
  &__box {
    border-radius: 24px;
    background: var(--main-orange, linear-gradient(251deg, #fe9215 33.97%, #ffb55f 95.83%));
    box-shadow: 11.36983px 11.36983px 19.89721px 0px rgba(0, 0, 0, 0.25);
    min-width: 800px;
    padding: 64px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
}

@media screen and (max-width: 992px) {
  .modal {
    &__box{
      min-width: auto;
      max-width: 70vw;
    }
  }
}
@media screen and (max-width: 576px) {
  .modal{
    &__box{
      padding: 30px;
    }
  }
}
</style>
