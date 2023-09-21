<template>
  <div class="card">
    <div class="card__photo">
      <div class="card__photo_big" v-if="images && images.length > 0">
        <img class="icon" src="../assets/gallery.svg" alt="" />
        <img :src="images[0].path" alt="Image" />
        <section>
          <div class="card__photo_small" v-for="(image, index) in images.slice(1)" :key="index">
            <img :src="image.path" alt="Image" />
          </div>

          <div class="card__photo_ph" v-if="images.length < 3">
            <img
              v-for="i in 3 - images.length"
              :key="i"
              :src="placeholderImage"
              alt="Placeholder"
            />
          </div>
        </section>
      </div>
      <div v-else>
        <img :src="placeholderImage" alt="Placeholder" />
      </div>
    </div>

    <div class="card__info">
      <div class="card__info_title" v-if="isSectionsVisible">
        <section>
          <h1>{{ name }}</h1>
          <h2>{{ address }}</h2>
        </section>
        <div class="geo" @click="toggleSectionsVisibility">
          <img src="../assets/geo.svg" alt="Geo" />
        </div>
        
      </div>
      <div class="card__info_data" v-if="isSectionsVisible">
        <section>
          <span>Занято номеров:</span>
          <span>Класс:</span>
          <span>Расположение:</span>
        </section>
        <section>
          <span>{{ freeRooms }} / {{ allRooms }}</span>
          <span>{{ roomClass }}</span>
          <span>{{ distanceFromCenter }}км от центра</span>
        </section>
      </div>
      <div class="card__info_map" v-if="!isSectionsVisible">
        <a
          :href="'https://yandex.ru/maps/67/tomsk/house/ulitsa_gertsena_46_1/bE0YfwFpTEcEQFtsfXh2cn9iZQ==/?ll=' + longitude + '%2C' + latitude + '&utm_medium=mapframe&utm_source=maps&z=17'"
          style="color:#eee;font-size:12px;position:absolute;top:14px;"
        ></a>
        <iframe
          :src="'https://yandex.ru/map-widget/v1/?ll=' + longitude + '%2C' + latitude + '&mode=whatshere&whatshere%5Bpoint%5D=' + longitude + '%2C' + latitude + '&whatshere%5Bzoom%5D=17&z=17'"
          width="560"
          height="400"
          frameborder="0"
          border-radius="80px"
          allowfullscreen="true"
          style="position:relative;"
        ></iframe>
        <div class="close" v-if="!isSectionsVisible" @click="toggleSectionsVisibility">
          <img src="../assets/close.svg" alt="Close" />
        </div>
      </div>

      <div class="card__info_others" v-if="isSectionsVisible">
        <span>от {{ sum }} р. за 1 день</span>
        <button>Подробнее</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from 'vue';

export default defineComponent({
  name: 'Card',
  props: {
    name: String,
    address: String,
    images: Array as PropType<{ path: string }[]>,
    placeholderImage: String,
    sum: Number,
    freeRooms: Number,
    allRooms: Number,
    roomClass: String,
    distanceFromCenter: String,
    latitude: String,
    longitude: String,
  },
  setup(props) {
    const isSectionsVisible = ref(true);

    const toggleSectionsVisibility = () => {
      isSectionsVisible.value = !isSectionsVisible.value;
    };

    return {
      isSectionsVisible,
      toggleSectionsVisibility,
    };
  },
});
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  margin: 16px;
  max-width: 1052px;
  border-radius: 8px;
  box-shadow: 3px 4px 4px 0px rgba(1, 0, 44, 0.25);
  justify-content: center;
  align-items: flex-start;
  background-color: #ffff;

  img {
    width: 100px;
  }

  &__info {
    display: flex;
    flex-direction: column;
    margin-left: 20px;
    padding: 16px;
    width: 400px;
    height: 240px;

    &_title {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;

      img {
        width: 48px;
        height: 48px;
        cursor: pointer;
      }

      section {
        display: flex;
        flex-direction: column;
        align-items: flex-start !important;
        margin-right: 20px;

        h1 {
          color: #00d56a;
          font-size: 18px;
          font-style: normal;
          font-weight: 400;
          line-height: normal;
          padding: 0;
          margin: 0;
          margin-bottom: 8px;
        }

        h2 {
          color: #01002c;
          font-size: 12px;
          font-style: normal;
          font-weight: 400;
          line-height: normal;
          padding: 0;
          margin: 0;
          margin-bottom: 28px;
        }
      }
    }

    &_data {
      display: flex;
      background-color: #f8f8ff;
      padding: 16px;
      gap: 16px;
      border-radius: 8px;
      justify-content: space-around;
      margin-bottom: 20px;

      span {
        color: #01002c;
        text-align: center;
        font-size: 12px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
      }

      span:not(:last-child) {
        margin-bottom: 16px;
      }
    }

    &_map {
      iframe {
        width: 390px;
        height: 240px;
        border-radius: 8px;

      }

      .close {
        position: absolute;
          img {
            width: 48px;
            height: 48px;
            cursor: pointer;
            transform: translate(715%, -508%);
          }
      }
    }

    section {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    &_others {
      display: flex;
      align-items: center;
      justify-content: space-between;

      span {
        font-size: 14px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;
      }

      button {
        color: white;
        background-color: #00d56a;
        width: 204px;
        height: 48px;
        text-align: center;
        border: none;
        border-radius: 8px;

        &:hover {
          background-color: #01002C;
          transition: 0.3s;
        }
      }
    }
  }

  &__photo {
    img {
      border-radius: 8px;
    }

    section {
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    &_big {
      display: flex;
      img {
        width: 413px;
        height: 240px;
        margin: 16px 6px 16px 16px;
      }

      .icon {
        position: absolute;
        width: 48px;
        height: 48px;
        transform: translateY(365%) translateX(33%);
      }
    }

    &_small img {
      width: 162px;
      height: 112px;
      object-fit: cover;
      margin: 6px;
    }

    &_ph img {
      width: 162px;
      height: 112px;
      margin: 6px;
    }
  }
  
}
</style>
