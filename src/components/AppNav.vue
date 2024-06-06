<script>
import $ from "jquery";

export default {
  name: "AppNav",
  mounted() {
    const navbarToggle = $("#navbarToggle");
    const navbarCollapse = $("#navbarSupportedContent");


    window.addEventListener('scroll', function() {
      const nav = document.querySelector('nav');
      const scrolledClass = 'scrolled';

      const scrollTop = window.scrollY;

      if (scrollTop === 0) {
        nav.classList.remove(scrolledClass);
      } else {
        nav.classList.add(scrolledClass);
      }
}); 

    // JavaScript per gestire il toggle del menu a tendina
    navbarToggle.on("click", function (event) {
      event.stopPropagation();
      navbarCollapse.toggleClass("show");
    });

    // Chiudi il menu a tendina quando si fa clic al di fuori di esso
    $(document).on("click", function (event) {
      var target = $(event.target);
      if (
        !target.closest("#navbarSupportedContent").length &&
        !target.is("#navbarToggle")
      ) {
        navbarCollapse.removeClass("show");
      }
    });
  },
};

</script>

<template>
  <nav class="navbar navbar-expand-md nunito-navbar">
    <div class="container-fluid my_container my_nav">
      <!-- Home Icon -->
      <router-link to="/">
        <a class="navbar-brand">
          <img src="\img\logo\pngegg.png" alt="" />
        </a>
      </router-link>
      <!-- Toggle button for mobile view -->
      <button class="navbar-toggler" type="button" id="navbarToggle" aria-controls="navbarSupportedContent"
        aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <div class="d-flex justify-content-between right-side ms-auto">
          <!-- Centered Navigation Links -->
          <div class="navbar-nav ms-auto w-100">
            <router-link class="text-decoration-none" to="/">
              <a class="nav-link text-center nav_voice" aria-current="page">Home</a>
            </router-link>
            <a class="nav-link text-center nav_voice" href="#">Pagamenti</a>
            <a class="nav-link text-center nav_voice" href="#">Contatti</a>
            <a class="nav-link text-center nav_voice" href="#">Su di noi</a>
            <span id="space"></span>
            <!-- Login Button -->
            <a class="text-center" href="http://127.0.0.1:8000">
              <button class="btn btn-sm ms-auto my_button" type="button">
                <span class=" text-capitalize"><i class="fa-solid fa-bell-concierge"></i> Ristoranti</span>
              </button>
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>



<style lang="scss" scoped>
@use "/src/variabiles.scss" as *;
@use "/src/mixins.scss" as *;

.nunito-navbar {
  font-family: "Nunito", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
}

.navbar {
  width: 100%;
  padding: 1rem 0;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
  background-color: $background_color_dark;

  position: fixed;
  top: 0;
  left: 0;
  z-index: 2;

  transition: all 0.3s linear;

  .my_nav {
    max-width: 1200px;

    button:focus:not(:focus-visible) {
      border: none;
    }

    .navbar-toggler {
      border: 1px solid $deactivated_text;
      border-radius: 10px;

      .navbar-toggler-icon {
        color: $deactivated_text;
      }
    }

    img {
      max-height: 5rem;
    }

    .right-side {

      a {
        font-weight: 700;
        position: relative;

        transition: all 0.5s linear;
      }

      .nav_voice {
        color: $text_color;
      }

      .nav_voice::after {
        content: "";
        position: absolute;
        width: 0;
        height: 5px;
        border-radius: 5px;
        display: block;
        margin-top: 5px;
        left: 50%;
        background: $secondary_color;
        transition: width 0.4s ease;
        -webkit-transition: width 0.4s ease;
        transform: translateX(-50%);
        transition: all 0.3s linear;
      }

      .nav_voice:hover::after {
        width: 75%;
      }


      .my_button {
        @include primary_button_style;

        font-weight: 600;
        border: none;

        margin-left: auto;
        margin-right: auto;

        font-size: 1.05rem;

        transition: all 0.3s linear;

        &:hover {
          background-color: $primary_color;
          color: $background_color;
        }

        span {
          font-weight: 800;
          
          i {
            font-size: 1.2rem;
            margin-right: .3rem;
          }
        }
      }
    }
  }

  #space {
    width: 3rem;
    height: 1rem;
  }
}

.scrolled {
    background-color: $secondary_color;
    box-shadow: none;

    a {
      color: $background_color;
    }

    .nav_voice::after {
      background-color: $background_color !important;
    }

    .my_button {
      background-color: $background_color !important;

      &:hover {
          background-color: $primary_color !important;
          color: $background_color !important;
        }
    }
  }


@media screen and (max-width: 767px) {

  .nav_voice:hover::after,
  .nav_voice.active::after {
    width: 15% !important;
  }
}
</style>
