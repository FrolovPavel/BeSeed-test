<template>
  <div class="card-statistics">
    <div class="card-statistics__top">
      <h3>{{mapTitle[title]}}</h3>
      <app-tooltip
        v-if="title != 'subscribers'"
        width="16"
        height="16"
      />
    </div>

    <div class="card-statistics__info">
      <base-icon
        :icon="title"
        width="32"
        height="32"
        viewBox="32"
      />
      <span>{{formatValue}}</span>
    </div>
  </div>
</template>

<script>
import BaseIcon from "@/components/Icons/BaseIcon";
import AppTooltip from "@/components/Tooltip";
export default {
  name: "AppCardStatistics",
  components: {AppTooltip, BaseIcon},

  data() {
    return {
      mapTitle: {
        subscribers: 'Подписчики',
        coverageER: 'ER охват',
        reactionsER: 'ER реакции',
        coveragePost: 'Охват поста',
        CTR: 'CTR'
      }
    }
  },
  props: {
    value: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      required: true
    }
  },
  computed: {
    formatValue() {
      if(Number.isInteger(this.value)) {
        return this.value.toLocaleString()
      }
      return this.value + '%'
    }
  }
}
</script>

<style lang="scss">
@import "../../../assets/scss/vars";

.card-statistics {
  padding: 16px;
  border-radius: $radiusMD;
  background-color: $grayscale100;
  width: 165px;

  &__top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 16px;

    h3 {
      color: $grayscale70;
      font-weight: 400;

    }
  }



  &__info {
    display: flex;
    align-items: center;
    gap: 8px;

    span {
      font-weight: 600;
      color: $darkBlue;
    }
  }
}
</style>
