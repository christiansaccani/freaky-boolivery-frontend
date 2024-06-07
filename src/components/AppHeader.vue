<script>
export default {
    name: "AppHeader",
    mounted() {
        const updateImageSource = () => {
            const imgHamb = document.querySelector('.img_hamb');
            if (window.innerWidth < 1005) {
                imgHamb.src = "/img/homepage/hamburger-responsive.png"; // Percorso alla nuova immagine
            } else {
                imgHamb.src = "/img/homepage/boolivery_hamburger_2.jpg";
            }
        };

        // Aggiorna l'immagine al caricamento della pagina e al ridimensionamento della finestra
        updateImageSource();
        window.addEventListener('resize', updateImageSource);
    }
};
</script>


<template>
    <div class="nunito-header">
        <div class="jumbotron gap-lg-0 row d-flex align-items-center">
            <div class="col-lg-6 col-12 h-100 d-flex justify-content-center">
                <div class="d-flex justify-content-center align-items-center jumbotron-content">
                    <img class="scream_img" src="/img/homepage/scream.png" alt="">
                    <h1 class="text-uppercase">Boolivery</h1>
                    <h2>Consegne da Paura!</h2>
                </div>
            </div>

            <div class="col-lg-6 col-12 justify-content-center p-0 m-0">
                <img class="img_hamb" src="" alt="">
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

    overflow-x: hidden;
}

.jumbotron {
    position: relative;
    background-color: $secondary_color;
    margin-top: 112px;
    padding-top: 1.5rem;
    padding-bottom: 3.5rem;

    gap: 1rem;
    overflow: hidden;

    @media screen and (min-width: 993px) {
        margin-top: 112px;
        padding-top: 0;
        padding-bottom: 0;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
    }

    .img_hamb {
    width: 100%;
    max-height: 25rem;
    object-fit: cover;

    border-top-left-radius: 197px;
    border-bottom-left-radius: 197px;

        @media (max-width: 992px) {
            bottom: 2rem;
            left: 50%;
            transform: translate(-50%, 50%);
            position: absolute;
            width: 9rem;
            height: 9rem;
            opacity: 0.32;
        }

        @media (max-width: 425px) {
            width: 7.5rem;
            height: 7.5rem;
            bottom: 1rem;
        }
    }   

    

    .jumbotron-content {

        display: flex;
        flex-direction: column;
        justify-content: start;
        text-align: start;
        color: $background_color;

        @media (max-width: 993px) {
            text-align: center !important;
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

        .scream_img {
            position: absolute;
            left: 1rem;
            top: -1rem;

            opacity: 0.15;
            object-fit: cover;

            @media (max-width: 992px) {
            
                transform: translateX(-50%) scale(0.7);
                top: -6.5rem;
                left: 50%;
            }

            @media (max-width: 425px) {
                transform: translateX(-50%) scale(0.55);
                top: -9rem;
                left: 50%;
            }
        }

        h1 {
            font-size: 6rem;
            letter-spacing: 4px;
            font-weight: 800;

            color: $text_color;
            z-index: 2;

            @media (max-width: 1215px) {
                padding-left: 1rem;
                font-size: 5rem;
            }

            @media (max-width: 425px) {
                font-size: 3rem;
            }
        }

        h2 {
            font-size: 2.5rem;
            font-weight: 700;
            color: $text_color;

            z-index: 2;

            @media (max-width: 425px) {
                font-size: 2rem;
            }
        }

        button {
            @include shopping_cart_button;

            &:hover {
                background-color: $primary_color;
                color: $background_color;
                transition: 0.3s ease;
                scale: 1.05;
            }
        }
    }
}
</style>