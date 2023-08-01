<template>
  <div class="tooltip">
    <div
      class="tooltip__icon"
      @mouseover="showTooltip"
      @mouseout="hideTooltip"
    >
      <base-icon
        icon="tooltip"
        :width="width"
        :height="height"
        :viewBox="viewBox"
      />
    </div>
    <Transition>
      <div
        v-if="isTooltip"
        class="tooltip__card"
      >
        подсказка
      </div>
    </Transition>

  </div>
</template>

<script>
import BaseIcon from "@/components/Icons/BaseIcon";
export default {
  name: "AppTooltip",
  components: {BaseIcon},
  props: {
    width: {
      type: [Number, String],
      default: 24
    },
    height: {
      type: [Number, String],
      default: 24
    },
    viewBox: {
      type: [Number, String],
      default: 24
    }
  },
  data() {
    return {
      isTooltip: false
    }
  },
  methods: {
    showTooltip() {
      this.isTooltip = true
    },
    hideTooltip() {
      this.isTooltip = false
    }
  }
}
</script>

<style lang="scss">
@import "../assets/scss/vars";

.tooltip {
  cursor: pointer;
  position: relative;

  &__icon {
    line-height: 0;
  }

  &__card {
    position: absolute;
    left: -50%;
    top: -42px;
    transform: translateX(-25%);
    background-color: $grayscaleWhite;
    padding: 8px;
    border-radius: $radiusSM;
    box-shadow: $shadow;
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

