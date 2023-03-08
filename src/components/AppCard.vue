<script>
export default {
  data() {
    return {
      stars: [],
    };
  },
  props: {
    title: String,
    originalTitle: String,
    language: String,
    vote: Number,
    pic: String,
    overview: String,
    cast: Array,
  },
  computed: {
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

    castList() {
      return this.cast.join();
    },
  },
  methods: {
    // Funzione per recuperare bandiera a seconda del codice country passato come parametro
    getFlag(country) {
      // Trasformo stringa in maiuscolo
      country = country.toUpperCase();

      // Gestisco i casi in cui la bandiera non viene trovata
      // bandiera inglese
      if (country == "EN")
        return "https://www.countryflagicons.com/FLAT/64/GB.png";
      // bandiera armena
      if (country == "HY")
        return "https://www.countryflagicons.com/FLAT/64/AM.png";
      // bandiera giapponese
      if (country == "JA")
        return "https://www.countryflagicons.com/FLAT/64/JP.png";
      // bandiera hong kong
      if (country == "ZH")
        return "https://www.countryflagicons.com/FLAT/64/HK.png";
      // bandiera corea del sud
      if (country == "KO")
        return "https://www.countryflagicons.com/FLAT/64/KR.png";
      // bandiera haiti
      if (country == "HI")
        return "https://www.countryflagicons.com/FLAT/64/HT.png";
      // bandiera repubblica ceca
      if (country == "CS")
        return "https://www.countryflagicons.com/FLAT/64/CZ.png";
      // bandiera georgia
      if (country == "KA")
        return "https://www.countryflagicons.com/FLAT/64/GE.png";

      // Ritorno tutte le altre bandiere
      return `https://www.countryflagicons.com/FLAT/64/${country}.png`;
    },
  },
};
</script>

<template>
  <li class="ms-0">
    <!-- CARD -->
    <div class="flip-box my-fade-from-bottom">
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
          <div v-else class="img-not-found">
            {{ title }}
          </div>
        </div>

        <!-- PARTE POSTERIORE CARD -->
        <div class="flip-box-back">
          <!-- TITLE -->
          <div>
            <span class="fw-semibold">TITLE: </span>
            <span class="fw-light">{{ title }}</span>
          </div>

          <!-- ORIGINAL TITLE, SE diverso dal titolo -->
          <div v-if="title != originalTitle" class="my-2">
            <span class="fw-semibold">ORIGINAL TITLE: </span>
            <span class="fw-light"> {{ originalTitle }} </span>
          </div>

          <!-- LANGUAGE -->
          <div class="my-2 text-center">
            <span class="fw-semibold">LANGUAGE: ({{ language }})</span>

            <!-- SE la bandiera non è quella inglese -->
            <div>
              <img :src="getFlag(language)" :alt="`${language} flag`" />
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

          <!-- CAST -->
          <div class="my-2">
            <span class="fw-semibold d-block">CAST: </span>
            <p class="fw-light">{{ castList }}</p>
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
      cursor: pointer;

      .flip-box-front,
      .flip-box-back {
        position: absolute;
        width: 100%;
        height: 100%;
        overflow-y: auto;
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
