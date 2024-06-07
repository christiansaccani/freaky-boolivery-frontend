<script>
export default {
  name: "AppFooter",

  components: {},

  data() {
    return {};
  },
};
</script>

<template>
  <footer>
    <!-- <hr class=""> -->
    <div class="container d-flex py-3">

      <div class="row d-flex flex-grow-1 gap-5 gap-sm-0 gap-md-0 inside-container">

        <div
          class="footer_links d-flex align-items-center col-4 flex-column py-3">
          <h5 class="pb-2">Termini Legali</h5>
          
          <div class="responsive_footer">
            <p class="ps-2">FAQ</p>
          
          
            <p class="ps-2">Centro Assistenza</p>
          
          
            <p class="ps-2">Informativa sulla Privacy</p>
          
          
            <p class="ps-2">Termini di Servizio</p>
          </div>
        </div>

        <div
          class="footer_links align-items-center d-flex col-4 flex-column py-3">
          <h5 class="pb-2">Feedback</h5>
          
          <div class="responsive_footer">
            <p>Aiutaci a migliorare</p>
          
          
            <p>Missione e visione</p>
          
          
            <p>Team</p>
          
          
            <p>Recensioni</p>
          </div>
        </div>


        <div
          class="footer_links social_media_contacts align-items-center d-flex col-4 flex-column py-3">
          <h5 class="pb-2">Seguici</h5>

          <div class="d-flex gap-2">
            <span>
              <a href="">
                <i class="fa-brands fa-twitter"></i>
              </a>
            </span>
            <span>
              <a href="">
                <i class="fa-brands fa-facebook"></i>
              </a>
            </span>
            <span>
              <a href="">
                <i class="fa-brands fa-instagram"></i>
              </a>
            </span>
            <span>
              <a href="">
                <i class="fa-brands fa-google-plus-g"></i>
              </a>
            </span>
            <span>
              <a href="">
                <i class="fa-brands fa-linkedin"></i>
              </a>
            </span>
          </div>



        </div>


      </div>



    </div>
  </footer>
</template>

<style lang="scss" scoped>
@use "/src/variabiles.scss" as *;
@use "/src/mixins.scss" as *;

footer {
  color: $deactivated_text;
  background-color: $primary_color;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.4);


  h5 {
    font-size: 1.2rem;
    font-weight: 500;
    color: $background_color;
  }


  img {
    height: 100px;
  }

  .primary-btn {
    @include primary_button_style;

    &:hover {
      background-color: $primary_color;
    }
  }

  .footer_links {


    p {

      font-size: 0.8rem;
      font-weight: 300;
      color: $deactivated_text;
      cursor: pointer;


      &:hover {
        color: $secondary_color;
      }
    }
  }

  .social_media_contacts {
    span {
      font-size: 1rem;
      color: $deactivated_text;

      a {
        color: $deactivated_text;

        &:hover {
          color: $secondary_color;
        }
      }
    }
  }
}

.my_text {
  color: $deactivated_text;
}

@media screen and (max-width: 767px) {

  h5 {
    font-size: 1.1rem !important;
  }

  footer {
    border-top-left-radius: 24px;
    border-top-right-radius: 24px;
  }

  .container {
    padding: 1.5rem !important;
  }

  .inside-container {
    flex-direction: column;
    align-items: center;

    width: 100% !important;
    gap: 0 !important;
  }

  .responsive_footer {

    display: flex;
    justify-content: center;

    gap: 1rem;

    p {
      white-space: nowrap;
    }
  }

  .footer_links {
    padding: 0 !important;
  }
}
</style>
