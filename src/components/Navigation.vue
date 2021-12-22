<template>
    <div
        class="navigation"
        :style="{
            background: 'rgba(0,0,0,' + backgroundOpacity + ')',
            transition: 'opacity 0.5s',
        }"
    >
        <div class="container">
            <div>
                <div class="hoodie-kidz-logo" @click="reloadPage"></div>
                <div></div>
                <div
                    class="hamburger-icon"
                    @click="menuOn"
                    v-if="!hamburgerDisplayed"
                ></div>
                <div
                    class="cross-icon"
                    @click="menuOff"
                    v-if="hamburgerDisplayed"
                ></div>
                <div class="nav-container">
                    <div class="discord"></div>
                    <div class="twitter"></div>
                    <a href="#about">About</a>
                    <a href="#starmap">Starmap</a>
                    <a href="#team">Team</a>
                    <a href="#faq">FAQ</a>
                    <a
                        href="#home"
                        style="font-weight: bold; color: gold"
                        @click="openMintMenu"
                        >MINT</a
                    >
                </div>
            </div>
        </div>
        <transition name="fade">
            <div
                class="hamburger-display"
                v-if="hamburgerDisplayed"
                @click="menuOff"
            >
                <a href="#about"><span class="purple">About</span></a>
                <a href="#starmap"><span class="salmon">Starmap</span></a>
                <a href="#team"><span class="orange">Team</span></a>
                <a href="#faq"><span class="pink">FAQ</span></a>
                <a
                    href="#home"
                    class=""
                    style="font-weight: bold; color: gold"
                    @click="openMintMenu"
                    ><span>MINT</span></a
                >
                <a><div class="discord"></div></a>
                <a><div class="twitter"></div></a>
            </div>
        </transition>
    </div>
</template>

<script>
import eventBus from "../eventBus";

export default {
    data() {
        return {
            backgroundOpacity: 0,
            hamburgerDisplayed: false,
        };
    },
    methods: {
        openMintMenu() {
            eventBus.$emit("open-mint-menu");
        },
        reloadPage() {
            document.location.reload();
        },
        menuOn() {
            this.hamburgerDisplayed = true;
            this.backgroundOpacity = 1;
        },
        menuOff() {
            this.hamburgerDisplayed = false;
            this.setParallax();
        },
        navigateTo() {
            this.menuOff();
        },
        setParallax() {
            var offsetTop = window.scrollY;
            var percent = offsetTop / 100;

            if (percent < 0) percent = 0;
            if (percent > 1) percent = 1;
            this.backgroundOpacity = percent;
        },
    },
    mounted() {
        window.addEventListener("scroll", this.setParallax);
        this.setParallax();
    },
    unmounted() {
        window.removeEventListener("scroll", this.setParallax);
    },
};
</script>

<style lang="scss">
.med-display {
    .nav-container {
        grid-gap: 2vh;
    }
}
.hamburger-display {
    transition: opacity 0.5s;
    position: fixed;
    z-index: 10000;
    top: 15vh;
    bottom: 0;
    display: grid;
    background: black;
    width: 100vw;
    align-content: stretch;
    padding-bottom: 50px;
    > * {
        width: 100%;
        display: flex;
        align-content: stretch;
        justify-content: center;
        align-items: center;

        > span {
            font-size: 30px;
        }
    }
}
.discord {
    background-image: url("../assets/Discord-Logo-White.svg");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 5vh;
    height: 5vh;
    min-width: 30px;
}
.twitter {
    background-image: url("../assets/twitter-logo-white.svg");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 5vh;
    height: 5vh;
    min-width: 35px;
}
.navigation {
    width: 100%;
    position: fixed;
    z-index: 10000;
    color: white;
    height: 15vh;
    a {
        text-decoration: none;
        color: white;
    }
    .container {
        margin: 0 !important;
        padding: 0 !important;

        > * {
            margin: 0 !important;
            padding: 0 !important;
            margin: 0 !important;
            height: 100%;
            padding: 0 !important;
            display: flex;
            flex-direction: column;
            align-content: flex-end;
            justify-content: center;
        }
    }
    .hoodie-kidz-logo {
        position: absolute;
        top: 0px;
        left: 0;
        width: 10vmin;
        bottom: 0px;
        background-repeat: no-repeat;
        background-size: contain;
        background-position: center;
        background-image: url("../assets/hoodie-kidz-logo.svg");
    }
    .hamburger-icon {
        position: absolute;
        top: -5px;
        right: 0;
        width: 8vmin;
        bottom: -5px;
        background-position: center;
        background-repeat: no-repeat;
        background-size: contain;
        background-origin: 50% 50%;
        background-image: url("../assets/icons/hamburger.svg");
    }
    .cross-icon {
        position: absolute;
        top: -5px;
        right: 0;
        width: 8vmin;
        bottom: -5px;
        background-position: center;
        background-repeat: no-repeat;
        background-size: contain;
        background-origin: 50% 50%;
        background-image: url("../assets/icons/cross.svg");
    }
}
.nav-container {
    display: flex;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
    font-weight: bold;
    text-align: center;
    grid-gap: 5px;
    align-content: flex-end;
    margin-left: 15vh;
    font-size: 25px;
    height: 100%;
    align-items: center;
    justify-content: flex-end;
    grid-gap: 3vh;
    flex-direction: row;
}

.small-display {
    .navigation {
        .container {
            > * {
                width: 100%;
            }
        }
        .hoodie-kidz-logo {
            left: 25px;
            width: 15vw;
        }
        .cross-icon,
        .hamburger-icon {
            right: 25px;
            width: 10vw;
        }
        .nav-container {
            display: none;
        }
    }
}
.small-horizontal-display {
    .navigation {
        .cross-icon,
        .hamburger-icon {
            display: none;
        }

        .hoodie-kidz-logo {
        }
        .nav-container {
            font-size: 18px;
        }
    }
}
.med-display {
    .navigation {
        .cross-icon,
        .hamburger-icon {
            display: none;
        }
    }
}
.large-display {
    .navigation {
        .cross-icon,
        .hamburger-icon {
            display: none;
        }
        .hoodie-kidz-logo {
        }
    }
}
</style>