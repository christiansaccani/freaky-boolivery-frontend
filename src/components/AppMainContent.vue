<script>
import axios from "axios";
import AppCardItem from "./AppCardItem.vue";

// import Swiper JS
import Swiper from "swiper";
// import Swiper styles
import "swiper/css";

const swiper = new Swiper(".swiper");

export default {
  name: "AppMainContent",

  components: {
    AppCardItem,
  },

  data() {
    return {
      baseApiUrl: "http://127.0.0.1:8000/api/",
      restaurants: [],
      types: [],
      checkButtonValue: [],
      apiLinks: [],
      // keeps track of current page
      apiPageNumber: 1,

      per_page: 1,
      last_page: 1,
      total_items: 1,

      // loader state
      isLoading: false,
    };
  },
  methods: {
    apiFilterTypes() {
      this.apiPageNumber = 1;
      // Chiama apiCall con i parametri aggiornati
      this.apiCall();
    },

    changePage(pageNumber) {
      // previous page
      if (pageNumber === "Prev" && this.apiPageNumber > 1) {
        this.apiPageNumber--;
      }
      // next page
      if (
        pageNumber === "Next" &&
        this.apiPageNumber < this.restaurants.last_page
      ) {
        this.apiPageNumber++;
      }
      // specific page
      if (!isNaN(pageNumber)) {
        this.apiPageNumber = parseInt(pageNumber); // Converti in numero intero
      }
      this.apiCall();
    },

    apiCall() {
      this.isLoading = true; // Set loader to true before making the API call

      const params = {
        // sets current page as parameter, by default it's 1
        page: this.apiPageNumber,
      };
      if (this.checkButtonValue.length > 0) {
        params.types = this.checkButtonValue.join(",");
      }
      axios
        .get(this.baseApiUrl + "restaurants", { params })
        .then((res) => {
          console.log(res);
          this.restaurants = res.data.results;
          this.apiLinks = res.data.results.links;
          this.per_page = res.data.results.per_page;
          this.last_page = res.data.results.last_page;
          this.total_items = res.data.results.total;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(() => {
          this.isLoading = false; // Set loader to false after the API call is completed
        });

      axios
        .get(this.baseApiUrl + "types")
        .then((res) => {
          this.types = res.data.results;
          console.log(this.baseApiUrl + "types");
          console.log(res.data.results);
          console.log(this.types);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

  mounted() {
    this.apiCall();
  },
};
</script>

<template>
  <section>
    <nav>
      <h3>Consigliati</h3>

      <button
        type="button"
        class="btn more"
        data-bs-toggle="modal"
        data-bs-target="#restaurantModal"
      >
        <span class="more-icon"
          ><i class="fa-solid fa-magnifying-glass"></i
        ></span>
        <span class="more-txt"> CATEGORIA</span>
      </button>

      <!-- Modal -->
      <div
        class="modal fade"
        id="restaurantModal"
        tabindex="-1"
        aria-labelledby="restaurantModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header my_modal_head">
              <h1
                class="modal-title fs-5 text-center"
                id="restaurantModalLabel"
              >
                Seleziona una o più categorie:
              </h1>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body my_modal_body">
              <div v-for="type in types" class="custom-checkbox">
                <input
                  class="form-check-input"
                  type="checkbox"
                  role="switch"
                  :value="type.type"
                  :id="type.type"
                  :name="type.type"
                  v-model="checkButtonValue"
                  @change="apiFilterTypes()"
                />
                <label
                  class="form-check-label custom-checkbox-label"
                  :for="type.type"
                  >{{ type.type }}</label
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <!-- CATEGORIE SELEZIONATE -->
    <div v-if="checkButtonValue.length != 0" class="food_selected">
      <h4>Categorie Selezionate:</h4>
      <div class="in_food_selected">
        <p class="type_res_button" v-for="category in checkButtonValue">
          {{ category }}
        </p>
      </div>
    </div>
    <!-- FINE -->

    <section id="cards_section">
      <div v-if="isLoading" class="loader"></div>

      <template
        v-else-if="
          restaurants && restaurants.data && restaurants.data.length > 0
        "
      >
        <AppCardItem
          v-for="restaurant in restaurants.data"
          :key="restaurant.id"
          :restaurant="restaurant"
        >
        </AppCardItem>
      </template>
      <div v-else>
        <h3>Nessun Ristorante trovato</h3>
      </div>
    </section>

    <div v-if="restaurants && restaurants.data && restaurants.data.length > 0">
      <vue-awesome-paginate
        :total-items="total_items"
        v-model="apiPageNumber"
        :items-per-page="per_page"
        :max-pages-shown="last_page"
        :on-click="changePage"
        :hide-prev-next-when-ends="true"
        paginate-buttons-class="paginate-buttons"
        active-page-class="active-page"
      />
    </div>
  </section>
</template>

<style lang="scss">
@use "/src/variabiles.scss" as *;
@use "/src/mixins.scss" as *;

section {
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;

  background-color: $background_color_dark;
  padding: 40px 0 35px;

  @media screen and (max-width: 425px) {
    padding: 30px 0 25px;
  }

  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;

    max-width: 1200px;
    width: 100%;

    h3 {

      font-size: 2.4rem;
      font-weight: 700;
      color: $text_color;
      cursor: default;

      .type_res_button {
        padding: 6px 12px;
        width: 8rem;
        border-radius: 20px;
        border: 1px solid $background_color;

        background-color: $background_color;
        color: $primary_color;
        font-weight: 600;

        transition: all 0.2s linear;

        &:hover {
          background-color: $secondary_color;
        }
      }

      .my_modal_body {
        display: flex;
        flex-flow: row wrap;
        justify-content: flex-start;
        width: 50%;
        row-gap: 3rem;
      }

      span {
        font-weight: normal;
      }
    }

    #food_types {
      display: flex;
      gap: 1rem;
    }

    .more {
      display: flex;
      justify-content: center;
      align-items: center;

      gap: .5rem;

      color: $background_color;
      background-color: $text_color;

      font-weight: 600;

      border: none;
      border-radius: 20px;

      padding: .5rem .6rem;
      width: 12rem;

      transition: all 0.2s linear;

        @media screen and (max-width: 1200px) {
          width: 6rem;
        }

      &:hover {
        background-color: $secondary_color;
        color: $text_color;
      }

      .more-txt {
        @media screen and (max-width: 1200px) {
          display: none;
        }
      }
    }

    .type_res_button {
      @include restaurant_button_style;

      &:hover {
        background-color: $secondary_color;
        color: $text_color;
      }
    }

    .my_modal_body {
      display: flex;
      flex-flow: row wrap;
      justify-content: space-around;
      width: 100%;
      row-gap: 0.5rem;
    }
  }

  #cards_section {
    display: flex;
    flex-flow: row;
    justify-content: center;
    align-items: center;

    gap: .5rem;
    padding-left: .5rem;
    padding-right: .5rem;

    width: 100%;
    max-width: 1200px;

    @media screen and (max-width: 425px) {
      gap: .4rem !important;
    }
  }

  .pagination-container {
    display: flex;
    column-gap: 10px;
    margin-top: 1rem;
  }

  .paginate-buttons {
    height: 40px;
    width: 40px;
    border-radius: 50%;
    cursor: pointer;
    background-color: rgb(242, 242, 242);
    border: 1px solid $text_color;
    color: black;

    font-weight: 600;
  }

  .paginate-buttons:hover {
    background-color: $secondary_color;
    color: $text_color;

    border: 1px solid $secondary_color;
  }

  .active-page {
    background-color: $secondary_color;
    border: 1px solid $secondary_color;
    color: $text_color;
  }

  .active-page:hover {
    background-color: $secondary_color;
  }

  .next-button,
  .back-button {
    background-color: $primary_color;
    color: $text_color_highlight;

    font-weight: 600;
  }

  /* ----- Modal Classes ----- */

  .custom-checkbox input[type="checkbox"] {
    display: none;
  }

  .custom-checkbox-label {
    @include restaurant_button_style;

    text-align: center;
  }

  .custom-checkbox input[type="checkbox"]:checked + .custom-checkbox-label {
    background-color: $secondary_color;
    color: $text_color;
  }

  .custom-checkbox-label:hover {
    background-color: $secondary_color;
    color: $text_color;
  }
}

.food_selected {
  margin-top: 1rem;

  .in_food_selected {
    display: flex;
    justify-content: center;
    align-items: center;

    gap: 5%;

    p {
      background-color: $secondary_color;
      color: $text_color;
      font-weight: 500;

      padding: 0.1rem 0.6rem;
      border-radius: 16px;

      cursor: default;
    }
  }
}

/* HTML: <div class="loader"></div> */
.loader {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 8px solid #d1914b;
  box-sizing: border-box;
  --c:no-repeat radial-gradient(farthest-side, #d64123 94%,#0000);
  --b:no-repeat radial-gradient(farthest-side, #000 94%,#0000);
  background:
    var(--c) 11px 15px,
    var(--b) 6px 15px,    
    var(--c) 35px 23px,
    var(--b) 29px 15px,    
    var(--c) 11px 46px,
    var(--b) 11px 34px,    
    var(--c) 36px 0px,
    var(--b) 50px 31px,
    var(--c) 47px 43px,
    var(--b) 31px 48px,    
    #f6d353; 
  background-size: 15px 15px,6px 6px;
  animation: l4 2s infinite;
}
@keyframes l4 {
  0%     {-webkit-mask:conic-gradient(#0000 0     ,#000 0)}
  16.67% {-webkit-mask:conic-gradient(#0000 60deg ,#000 0)}
  33.33% {-webkit-mask:conic-gradient(#0000 120deg,#000 0)}
  50%    {-webkit-mask:conic-gradient(#0000 180deg,#000 0)}
  66.67% {-webkit-mask:conic-gradient(#0000 240deg,#000 0)}
  83.33% {-webkit-mask:conic-gradient(#0000 300deg,#000 0)}
  100%   {-webkit-mask:conic-gradient(#0000 360deg,#000 0)}
}

/* ----- RESPONSIVE ----- */

@media screen and (max-width: 1200px) {
  h3 {
    padding-left: .5rem;
  }

  section nav .more {
    border-top-right-radius: 0px;
    border-bottom-right-radius: 0px;
  }

  section nav #food_types {
    background-color: $background_color;
    border-radius: 20px;
    gap: 0;
  }

  section nav .type_res_button:not(:first-child):not(:last-child) {
    border-radius: 0px;
  }

  section nav .type_res_button:first-child {
    border-top-right-radius: 0px;
    border-bottom-right-radius: 0px;
  }

  section nav .type_res_button:last-child {
    border-top-left-radius: 0px;
    border-bottom-left-radius: 0px;
  }
}

@media screen and (max-width: 946px) {
  #cards_section {
    flex-flow: row wrap !important;
    row-gap: 2rem !important;
  }
}

@media screen and (max-width: 992px) {
  section {
    padding-top: 2rem;
  }

  section nav #food_types {
    background-color: $background_color_dark;
    border-radius: 20px;

    justify-content: space-around;
    width: 100%;
  }

  section nav .type_res_button:not(:first-child):not(:last-child) {
    border-radius: 20px;
  }

  section nav .type_res_button:first-child {
    border-top-right-radius: 20px;
    border-bottom-right-radius: 20px;
  }

  section nav .type_res_button:last-child {
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;
  }

  section nav .type_res_button {
    width: 10rem;
  }
}

@media screen and (max-width: 768px) {
  section nav .type_res_button {
    width: 6rem;
  }
}
</style>
