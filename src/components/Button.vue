<template>
  <button
    class="button"
    :class="`button--${view}`"
    @click="$emit('click')"
  >
    <base-icon
      v-if="icon"
      :icon="icon"
      :width="width"
      :height="height"
      class="button__icon"
    />
    <slot />
  </button>
</template>

<script>
import BaseIcon from "@/components/Icons/BaseIcon";
export default {
  name: "AppButton",
  components: {BaseIcon},
  props: {
    view: {
      type: String,
      required: false
    },
    icon: {
      type: String,
      required: false
    },
    width: {
      type: String,
      required: false
    },
    height: {
      type: String,
      required: false
    }
  }
}
</script>

<style lang="scss">
@import "../assets/scss/vars";

.button {
  font-size: 16px;
  line-height: 22px;
  padding: 11px 24px;
  border-radius: $radiusSM;
  white-space: nowrap;
  transition: 0.3s background-color;

  &--icon {
    background: transparent;
    padding: 0;
    line-height: 0;
  }

  &--light-blue {
    background-color: $lightBlueButton;
    color: $darkBlue;

    @include hover {
      background-color: rgba(0, 133, 210, 0.40);
    }
  }

  &--blue {
    background-color: $blue;
    color: $grayscaleWhite;

    @include hover {
      background-color: $blueHover;
    }

    &:active {
      background-color: $blueClick;
    }
  }

  &--light-green {
    background: $greenLight;
    color: $green;

    @include hover {
      background-color: $greenHover;
    }

    &:active {
      background-color: $greenClick;
    }
  }
}
</style>
