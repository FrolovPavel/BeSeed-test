<template>
  <Transition>
    <div
      v-if="isShow"
      class="modal"
    >
      <div class="modal__overlay">
        <div class="modal__card">
          <slot />
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  name: "AppModalWrapper",
  props: {
    isShow: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style lang="scss">
@import "../../assets/scss/vars";

.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  &__overlay {
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.15);
  }

  &__card {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 36px;
    border-radius: $radiusLG;
    background-color: $grayscaleWhite;
    box-shadow: $shadow;

    @media (max-width: 1077px) {
      overflow: auto;
      border-radius: 0;
      top: 0;
      left: 0;
      transform: none;
      width: 100%;
      height: 100%;
    }

    @media (max-width: 649px) {
      padding: 16px;
    }
  }
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

</style>
