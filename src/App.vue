<template>
  <div>
    <app-button
      view="light-blue"
      @click="openModal"
    >
      Подробнее
    </app-button>
    <app-modal-site-preview
      :isShow="isModal"
      :modalData="mockModalData"
      @close="closeModal"
    />
  </div>
</template>

<script>


import AppButton from "@/components/Button";
import AppModalSitePreview from "@/components/Modals/SitePreview/ModalSitePreview";
export default {
  name: 'App',
  components: {AppModalSitePreview, AppButton},
  data() {
    return {
      isModal: false,
      mockModalData: {
        title: 'Стартапы и бизнес',
        confirmed: true,
        description: `vc.ru — крупнейшая в рунете площадка для предпринимателей нового поколения.
                      Сайт для тех, кому интересен бизнес в России и мире, технологии, модели роста,
                      стартапы и компании покрупнее, неординарные герои, развитие рынков и различных сфер.`,
        image: 'http://pics.wikireality.ru/upload/1/15/Vc_ru.jpg',
        info: {
          theme: ['Бизнес', 'Доска объявлений', 'Дизайн и интерьер', 'Строительство', 'Тематика 1', 'Тематика 2', 'Тематика 3'],
          languages: ['Русский'],
          countries: ['Россия', 'Украина', 'Беларусь'],
          ageAudiences: '18-52',
          sexRatio: '40/60',
          isAuthorPlatform: true
        },
        statistics: {
          subscribers: 1000000,
          coverageER: 35.8,
          reactionsER: 35.8,
          coveragePost: 1000000,
          CTR: 35.8
        }
      }
    }
  },
  methods: {
    openModal() {
      this.isModal = true
    },
    closeModal() {
      this.isModal = false
    }
  }
}
</script>

<style>
@import './assets/scss/main.scss';
</style>
