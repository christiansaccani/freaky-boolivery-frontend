<script>

export default {
    name: "AppHeader",
};

</script>

<template>
    <div class="nunito-header">

        <div class="jumbotron gap-lg-0 row d-flex align-items-center">

            <div class="col-lg-6 col-12 h-100 d-flex justify-content-center">
                <div class="d-flex justify-content-center jumbotron-content">
                    <h1 class="text-uppercase">Boolivery</h1>
                    <h2 class="text-capitalize">Consegne da Paura...</h2>
                    <h3 class="text-capitalize">... ad emissioni Zero!</h3>
                </div>
            </div>

            <div class="col-lg-6 col-12 justify-content-center p-0 m-0">
                <img src="/img/homepage/boolivery_hamburger_2.jpg" alt="">
            </div>

        </div>

    </div>
</template>

<style lang="scss" scoped>
@use "/src/variabiles.scss" as *;
@use "/src/mixins.scss" as *;

.nunito-header {
    font-family: "Nunito", sans-serif;
    font-optical-sizing: auto;
    font-style: normal;
}

.jumbotron {
    position: relative;
    background-color: $secondary_color;
    margin-top: 112px;
    padding-top: 1.5rem;

    padding-bottom: 3.5rem;

    gap: 1rem;

    @media screen and (min-width: 992px) {
        margin-top: 112px;
        padding-top: 0;
        padding-bottom: 0;
        border-top-left-radius: 1rem;
        border-top-right-radius: 100px;
        border-bottom-right-radius: 1rem;
        border-bottom-left-radius: 1rem;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
    }

    img {
    width: 100%;
    max-height: 25rem;
    object-fit: cover;

    transform-origin: top;

        @media (max-width: 992px) {
            bottom: 0;
            left: 50%;
            transform: translate(-50%, 50%);
            position: absolute;
            width: 9rem;
            height: 9rem;
            border-radius: 50%;

            border: 3px solid $secondary_color;

            transition: all 1s linear;

            &:hover {
                transform: translate(-50%, 50%) rotateY(360deg);
            }
        }
    }   

    

    .jumbotron-content {

        display: flex;
        flex-direction: column;
        justify-content: start;
        text-align: start;
        color: $background_color;

        @media (max-width: 992px) {
            text-align: center;
        }

        animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
        animation-delay: 0.3s;

        @keyframes tracking-in-expand {
            0% {
                letter-spacing: -0.5em;
                opacity: 0;
            }

            40% {
                opacity: 0.6;
            }

            100% {
                opacity: 1;
            }
        }

        h1 {
            font-size: 4rem;
            font-weight: 800;

            color: $text_color;

            @media (max-width: 375px) {
                font-size: 3rem;
            }
        }

        h2 {
            font-size: 2.5rem;
            font-weight: 700;
            color: $text_color;

            @media (max-width: 394px) {
                font-size: 2rem;
            }
        }

        h3 {
            color: $text_color;
            font-weight: 700;
        }

        button {
            @include shopping_cart_button;

            &:hover {
                background-color: $primary_color;
                color: #ffffff;
                transition: 0.3s ease;
                scale: 1.05;
            }

        }

    }

}
</style>