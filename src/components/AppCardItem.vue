<script>
export default {
  name: "AppCardItem",
  components: {},

  props: {
    restaurant: Object,
  },

  data() {
    return {};
  },
};
</script>

<template>
  <router-link
        :to="{ name: 'restaurant', params: { id: restaurant.id } }"
        class="card my_card gap-1">
    <div class="img-container">
      <img
        v-if="restaurant.image"
        :src="
          restaurant.image.startsWith('http')
            ? restaurant.image
            : 'http://localhost:8000/storage/' + restaurant.image
        "
        class="card-img-top"
        alt="..."
      />
      <img
        v-else
        class="card-img-top"
        src="/img/homepage/placeholdertemp.jpg"
        alt="..."
      />
      <div class="types-pill">
        <span v-for="type in restaurant.types">
           {{ type.type }}
        </span>
      </div>
    </div>

    <div class="card-body">
      <h5 class="card-title text-start">{{ restaurant.name }}</h5>

      <btn class="btn btn-primary my_btn">
        <i class="fa-solid fa-person-biking"></i>
      </btn>
    </div>
  </router-link>
</template>

<style lang="scss" scoped>
@use "/src/variabiles.scss" as *;
@use "/src/mixins.scss" as *;

.my_card {
  border-radius: 24px;
  border-color: transparent;
  color: $text_color;

  max-width: 305px;
  width: 100%;

  background-color: $background_color_dark;

  cursor: pointer;
  text-decoration: none;

  .img-container {

    position: relative;

    img {
      border-radius: 16px;
      object-fit: cover;

      height: 10rem;

      box-shadow: 3px 3px 3px rgba(20, 20, 20, 0.15);
    }

    .types-pill {
    position: absolute;
    left: 10px;
    bottom: 10px;
    right: auto;

    display: flex;
    flex-wrap: wrap;

    @media screen and (max-width: 425px) {
      left: auto;
      right: 10px;
    }

    span {
      font-weight: 500;
      background-color: $secondary_color;
      color: $text_color;
      border: 1px solid $text_color;
      padding: 0.1rem 0.5em;
      border-radius: 18px;
      margin: 0.1rem;

      opacity: 0.90;
    }
  }

  }

  .card-body {
    padding: 0.5rem 0 0;
  }

  .restaurant_type {
    display: flex;
    justify-content: center;
    margin-bottom: 1.5rem;
    margin-top: 0.5rem;

    span {
      font-weight: 500;

      color: $background_color;
      background-color: $primary_color;

      padding: 0.1rem 0.6rem;
      border-radius: 16px;
    }
  }

  .card-title {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    line-height: 1.8rem;
    padding-left: .2rem;

    color: $text_color;
    text-shadow: 2px 2px 4px rgba(242, 202, 57, 0.3);

    @media screen and (max-width: 425px) {
      position: absolute;
      top: 10px;
      left: 10px;

      color: $background_color;
      background-color: $text_color;
      padding: 0.1rem 0.6rem;
      border-radius: 12px;
    }
  }

  .my_btn {
    position: absolute;
    bottom: 0%;
    right: 5%;
    transform: translate(0%, 30%);

    border-radius: 50%;
    padding: .6rem .7rem;

    transition: all 0.2s linear;
    background: linear-gradient(to bottom right, #f2ca39, #eeba00);
    color: $background_color;
    border: none;

    box-shadow: 5px 5px 5px rgba(20, 20, 20, 0.15);

    @media screen and (max-width: 425px) {
      display: none;
    }
  }
}

.my_card:hover .my_btn{
  transform: translate(0%, 30%) scale(1.1);
}

@media screen and (min-width: 946px) and (max-width: 1200px) {
  .my_btn {
    display: none;
  }
}

@media screen and (max-width: 946px) {
  .my_card {
    max-width: 372px;
  }
  
}

@media screen and (max-width: 768px) {
  .my_card {
    max-width: 452px;
  }
  
}
</style>
