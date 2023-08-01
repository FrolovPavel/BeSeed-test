<template>
 <app-modal-wrapper :isShow="isShow" >
   <div class="modal-preview">
     <div class="modal-preview__top">
       <div class="modal-preview__info">
         <div class="modal-preview__description">
           <img
             class="modal-preview__image"
             :src="modalData.image"
             alt="icon-site"
           >
           <div class="modal-preview__description-inner">
             <h1 class="modal-preview__title">
                <base-icon
                  v-if="modalData.confirmed"
                  class="modal-preview__confirmed"
                  icon="confirmed"
                  width="32"
                  height="32"
                />
               {{modalData.title}}
             </h1>
             <a
               href="https://vk.com"
               class="modal-preview__link"
               target="_blank"
             >
               <base-icon
                icon="vk"
                viewBox="20"
                width="20"
                height="20"
               />
               Ссылка на площадку
             </a>
             <p class="modal-preview__text">
               {{description}}
               <span v-if="adaptiveNotebook">показать все</span>
             </p>
           </div>
         </div>
         <div class="modal-preview__details">
           <h2>Информация о площадке</h2>
           <ul>
             <li class="modal-preview__detail">
               <span>Тематика площадки</span>
               <span class="modal-preview__separator"></span>
               {{theme}}
               <span
                 v-if="themRemained"
                 class="modal-preview__remain"
               >
                 &nbsp;&nbsp;еще {{themRemained}}
               </span>
             </li>
             <li class="modal-preview__detail">
               <span>Языки</span>
               <span class="modal-preview__separator"></span>
               {{modalData.info.languages.join(', ')}}
             </li>
             <li class="modal-preview__detail">
               <span>Страны</span>
               <span class="modal-preview__separator"></span>
               {{modalData.info.countries.join(', ')}}
             </li>
             <li class="modal-preview__detail">
               <span>Возраст аудитории</span>
               <span class="modal-preview__separator"></span>
               {{modalData.info.ageAudiences}}
             </li>
             <li class="modal-preview__detail">
               <span>Соотношение полов (М/Ж), %</span>
               <span class="modal-preview__separator"></span>
               {{modalData.info.sexRatio}}
             </li>
             <li class="modal-preview__detail">
               <span>Авторская площадка</span>
               <span class="modal-preview__separator"></span>
               {{modalData.info.isAuthorPlatform ? 'Да' : 'Нет'}}
             </li>
           </ul>
         </div>
       </div>
       <app-formats-place />
     </div>
    <div class="modal-preview__bottom">
      <h2>Статистика площадки</h2>
      <div class="modal-preview__statistics">
        <app-card-statistics
          v-for="(value, key) in modalData.statistics"
          :key="key"
          :value="value"
          :title="key"
        />
        <app-button
          class="modal-preview__close"
          icon="close"
          view="icon"
          width="32"
          height="32"
          @click="$emit('close')"
        />
      </div>
    </div>
   </div>
 </app-modal-wrapper>
</template>

<script>
import AppModalWrapper from "@/components/Modals/ModalWrapper";
import BaseIcon from "@/components/Icons/BaseIcon";
import AppFormatsPlace from "@/components/Modals/SitePreview/FormatsPlace";
import AppCardStatistics from "@/components/Modals/SitePreview/CardStatistics";
import AppButton from "@/components/Button";
export default {
  name: "AppModalPreview",
  components: {AppButton, AppCardStatistics, AppFormatsPlace, BaseIcon, AppModalWrapper},
  props: {
    isShow: {
      type: Boolean,
      required: true
    },
    modalData: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      widthWindow: window.innerWidth,
    }
  },
  computed: {
    theme () {
      let themes = this.modalData.info.theme
      let result = ''
      const maxLength = this.adaptiveNotebook
        ? this.adaptiveMobile ? 10 : 40
        : 58

      for(let theme of themes) {
        if(result.length > maxLength && this.adaptiveNotebook) {
          result = result.substring(0, maxLength) + '...'
          return result
        }

        if(result.length + theme.length > maxLength && !this.adaptiveNotebook) {
          result = result.substring(0, result.lastIndexOf(","))
          return result
        }
        result += theme + ', '
      }
      return result
    },
    themRemained () {
      return this.modalData.info.theme.length - this.theme.split(', ').length
    },
    description() {
      const maxLength = 205

      if(this.adaptiveNotebook) {
        return this.modalData.description.substring(0, maxLength) + '...'
      }

      return this.modalData.description
    },
    adaptiveNotebook () {
      return this.widthWindow < 1500
    },
    adaptiveMobile () {
      return this.widthWindow < 650
    }
  },
  methods: {
    setInnerWidth() {
      this.widthWindow = window.innerWidth
    }
  },
  mounted() {
    window.addEventListener('resize', this.setInnerWidth)
  }
}
</script>

<style lang="scss">
@import "../../../assets/scss/vars";

.modal-preview {

  &__top {
    display: flex;
    align-items: flex-start;
    margin-bottom: 32px;

    @media (max-width: 1077px) {
     flex-direction: column;
    }
  }

  &__info {
    margin-right: 140px;
    width: 760px;
    flex-shrink: 0;

    @media (max-width: 1499px) {
      margin-right: 60px;
      width: 600px;
    }

    @media (max-width: 1077px) {
      margin-right: 0;
      width: 100%;
      margin-bottom: 32px;
    }
  }

  &__description {
    display: flex;
    align-items: flex-start;
    margin-bottom: 32px;

    @media (max-width: 649px) {
      flex-direction: column-reverse;
    }
  }

  &__image {
    display: inline-block;
    min-width: 184px;
    height: 184px;
    border-radius: $radiusMD;
    margin-right: 24px;

    @media (max-width: 649px) {
      width: 100%;
      height: auto;
      margin-top: 16px;
    }
  }

  &__title {
    display: flex;
    align-items: center;
    gap: 8px;
    color: $darkBlue;
    font-size: 32px;
    line-height: 40px;
    white-space: nowrap;
    margin-bottom: 24px;

    @media (max-width: 649px) {
      font-size: 24px;
    }
  }

  &__link {
    display: flex;
    align-items: center;
    gap: 8px;
    color: $blue;
    margin-bottom: 8px;
  }

  &__text {
    color: $darkBlue;
    span {
      color: $blue;
    }
  }

  &__details {
    h2 {
      color: $darkBlue;
      font-size: 20px;
      line-height: 28px;
      white-space: nowrap;
      margin-bottom: 16px;
    }
  }

  &__detail {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    white-space: nowrap;
    color: $darkBlue;

    &:not(:last-child) {
      margin-bottom: 8px;
    }

    span:first-child {
      color:  $grayscale70;
    }
  }

  &__separator {
    display: inline-block;
    width: 100%;
    height: 1px;
    margin: 0 4px;
    transform: translateY(-5px);
    background: url("../../../../src/assets/dashed.svg");

  }

  &__remain {
    color: $blue;
  }

  &__bottom {
    h2 {
      font-size: 20px;
      font-weight: 600;
      line-height: 28px;
      color: $darkBlue;
      margin-bottom: 16px;
    }
  }

  &__statistics {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 16px;
  }

  &__close {
    margin-top: auto;
    margin-left: auto;
  }
}
</style>
