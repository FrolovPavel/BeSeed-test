<template>
  <div class="formats">
    <div class="formats__top">
      <h2>Форматы размещения</h2>
      <app-tooltip />
    </div>
    <div class="formats__grid">
      <ul>
        <li>
          <span>Формат</span>
          <span>Без закрепления</span>
          <span>С закреплением</span>
        </li>
        <li>
          <span>1/24</span>
          <span>500 ₽</span>
          <span>50 000 ₽</span>
        </li>
        <li>
          <span>1/48</span>
          <span>5 000 ₽</span>
          <span>550 000 ₽</span>
        </li>
        <li>
          <span>1/72</span>
          <span>50 000 ₽</span>
          <span>1 000 000 ₽</span>
        </li>
      </ul>
    </div>
    <div class="formats__buttons">
      <div
        v-if="isAddCart"
        class="formats__buttons-cart"
      >
        <app-button view="light-green">
          Площадка в корзине
        </app-button>
        <app-button view="blue">
          Перейти в корзину
        </app-button>
      </div>
      <app-button
        v-else
        class="formats__add"
        view="blue"
        @click="isAddCart = true"
      >
        Добавить площадку в корзину
      </app-button>
    </div>
    <div class="formats__info">
      Выбрать формат и настроить параметры размещения вы сможете в Корзине
    </div>
  </div>
</template>

<script>
import AppTooltip from "@/components/Tooltip";
import AppButton from "@/components/Button";
export default {
  name: "AppFormatsPlace",
  components: {AppButton, AppTooltip},
  data() {
    return {
      isAddCart: false
    }
  }
}
</script>

<style lang="scss">
@import "../../../assets/scss/vars";

.formats {
  padding: 24px;
  background-color: $lightBlue;
  border-radius: $radiusMD;
  max-width: 468px;

  @media (max-width: 1077px) {
    width: 100%;
    max-width: unset;
  }

  &__top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 16px;

    h2 {
      font-size: 24px;
      line-height: 32px;
      color: $darkBlue;

      @media (max-width: 649px) {
        font-size: 20px;
      }
    }
  }

  &__grid {
    margin-bottom: 24px;

    li {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: $grayscaleWhite;
      padding: 8px;
      border-radius: $radiusSM;

      &:first-child {
        background-color: transparent;
        color: $grayscale70;

        span {
          font-weight: 400;

          @media (max-width: 649px) {
            width: 100px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
          }

          &:nth-child(2) {
            width: 134px;
          }
        }
      }

      span:nth-child(2) {
        width: 159px;
        text-align: right;
      }

      span:nth-child(3) {
        width: 128px;
        text-align: right;
      }

      span + span {
        font-weight: 600;
      }

      &:not(:last-child) {
        margin-bottom: 8px;
      }
    }
  }

  &__buttons {
    margin-bottom: 8px;
  }

  &__buttons-cart {
    display: flex;
    gap: 8px;
  }

  &__add {
    width: 100%;
  }

  &__info {
    text-align: left;
    color: $grayscale70;
  }
}

</style>
