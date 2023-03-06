<script>
export default {
  data() {
    return {
      stars: [],
    };
  },
  props: {
    name: String,
    originalName: String,
    language: String,
    vote: Number,
    pic: String,
    overview: String,
  },
  computed: {
    toUpperCaseLanguage() {
      return this.language.toUpperCase();
    },
    halfNumber() {
      return Math.ceil(this.vote / 2);
    },
    getStars() {
      // Aggiungo stelle piene
      for (let i = this.halfNumber; i >= 1; i--) {
        this.stars.push("fa-solid fa-star");
      }

      // Aggiungo stelle vuote
      for (let i = 5 - this.halfNumber; i >= 1; i--) {
        this.stars.push("fa-regular fa-star");
      }
      return this.stars;
    },
  },
};
</script>

<template>
  <li class="ms-0">
    <!-- CARD -->
    <div class="flip-box">
      <!-- CONTENUTO CARD -->
      <div class="flip-box-inner">
        <!-- PARTE FRONTALE CARD -->
        <div class="flip-box-front">
          <!-- SE viene trovata l'immagine dall'API -->
          <img
            v-if="pic"
            :src="`https://image.tmdb.org/t/p/w342${pic}`"
            class="poster-img"
          />

          <!-- ALTRIMENTI -->
          <div class="img-not-found" v-else>
            {{ name }}
          </div>
        </div>

        <!-- PARTE POSTERIORE CARD -->
        <div class="flip-box-back">
          <!-- TITLE -->
          <div>
            <span class="fw-semibold">TITLE: </span>
            <span class="fw-light">{{ name }}</span>
          </div>

          <!-- ORIGINAL TITLE, SE diverso dal titolo -->
          <div v-if="originalName != name" class="my-2">
            <span class="fw-semibold">ORIGINAL TITLE: </span>
            <span class="fw-light"> {{ originalName }} </span>
          </div>

          <!-- LANGUAGE -->
          <div class="my-2 text-center">
            <span class="fw-semibold">LANGUAGE: ({{ language }})</span>

            <!-- SE la bandiera non è quella inglese -->
            <div v-if="language != 'en'">
              <img
                :src="`https://www.countryflagicons.com/FLAT/64/${toUpperCaseLanguage}.png`"
                :alt="`${language} flag`"
              />
            </div>

            <!-- SE la bandiera è quella inglese -->
            <div v-else-if="(language = 'en')">
              <img
                src="https://www.countryflagicons.com/FLAT/64/GB.png"
                :alt="`${language} flag`"
              />
            </div>
          </div>

          <!-- VOTE -->
          <div class="my-2 text-center">
            <span class="fw-semibold d-block">VOTE: </span>
            <span v-for="star in getStars" class="star">
              <font-awesome-icon :icon="star" />
            </span>
          </div>

          <!-- OVERVIEW -->
          <div class="my-2 overview-text">
            <span class="fw-semibold d-block">OVERVIEW: </span>
            <p class="fw-light">{{ overview }}</p>
          </div>
        </div>
      </div>
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  width: 300px;

  .flip-box {
    background-color: transparent;
    width: 300px;
    height: 450px;
    perspective: 1000px;

    .flip-box-inner {
      position: relative;
      width: 100%;
      height: 100%;
      transition: transform 0.8s;
      transform-style: preserve-3d;

      .flip-box-front,
      .flip-box-back {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        -webkit-backface-visibility: hidden; /* Safari */

        .poster-img {
          width: 100%;
          height: 100%;
        }

        .img-not-found {
          background-color: rgba(20, 20, 20, 0.7);
          width: 100%;
          height: 100%;
          display: flex;
          justify-content: center;
          align-items: center;
          color: #fff;
          font-size: 2rem;
          font-weight: bold;
        }
      }

      .flip-box-back {
        background-color: #111;
        color: white;
        transform: rotateY(180deg);

        .fw-light {
          color: #bbb;
        }

        .star {
          color: yellow;
        }

        .overview-text {
          max-height: 8rem;
          overflow-y: auto;
          text-align: center;
        }
      }
    }

    &:hover .flip-box-inner {
      transform: rotateY(-180deg);
    }
  }
}
</style>
