<template>
    <section class="minting-section">
        <div class="container">
            <div class="minting-text-top">
                <div
                    style="
                        grid-area: a;
                        display: flex;
                        align-content: center;
                        justify-content: center;
                        position: relative;
                        flex-wrap: wrap;
                    "
                >
                    <p>Join the coolest kidz in the land of Gooo</p>
                </div>
                <mint-button></mint-button>
                <div style="grid-area: c">
                    <p>
                        By minting a
                        <span class="important">Hoodie Kid</span> you will
                        become <span class="gold">patron</span> of a passionate
                        creative team ready to give it all in the future of the
                        blockchain. <span class="important">The team</span> will
                        then reward <span class="gold">patrons</span> by
                        providing them with <span class="gold">perks</span> in
                        coming projects and events.
                    </p>
                    <h2>DO YOU PLAY TO EARN?</h2>
                    <p>
                        <span class="important">The first project</span> is a
                        <span class="epic">"play to earn" videogame</span> and
                        the related <span class="gold">perks</span> will be
                        initial
                        <span class="epic">
                            in-game items in form of exclusive NFTs</span
                        >.
                    </p>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import MintButton from "./MintButton.vue";
export default {
    data() {
        return {
            offset_0: 0,
            offset_1: 0,
            offset_2: 0,
            offset_3: 0,
            black: 0,
            initial_scroll: 0,
        };
    },
    methods: {},
    mounted() {},
    components: {
        MintButton,
    },
};
</script>

<style lang="scss">
.small-display {
    .minting-section {
        .minting-text-top {
            grid-template-columns: 1fr;
            grid-template-rows: 15vh 15vh auto;
            grid-template-areas:
                " b "
                " a "
                " c ";
            h2 {
                text-align: left;
                font-weight: bolder;
                font-size: 30px;
                padding: 0 30px 0 30px;
            }
            h3 {
                text-align: left;
                font-size: 23px;
                padding: 0 30px 0 30px;
            }

            p {
                text-align: justify;
                font-size: calc(20px + 0.2vw);
                padding: 0px 30px 0 30px;
                line-height: calc(30px + 0.2vw);
            }
        }
    }
}
.small-horizontal-display {
    .minting-section {
        .container {
            padding-top: 8vh;
        }
        .minting-text-top {
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 20vh auto;
            grid-template-areas:
                " a b "
                " c c ";
            h2 {
                text-align: left;
                font-weight: bolder;
                font-size: 40px;
                padding: 20px 0 0 0;
            }
            h3 {
                text-align: left;
                font-size: 20px;
                padding: 0;
            }

            p {
                text-align: justify;
                font-size: calc(20px+0.5vw);
                padding: 0;
            }
            .minting-screen {
                margin: 0 0 0 30px;
            }
        }
    }
}
.med-display {
    .minting-section {
        .minting-text-top {
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 20vh auto;
            grid-template-areas:
                " a b "
                " c c ";
            h2 {
                text-align: left;
                font-weight: bolder;
                font-size: calc(40px + 1vh);
                padding: 50px 0 0 0;
            }
            h3 {
                text-align: left;
                font-size: calc(30px + 0.5vh);
                padding: 15px 0 0 0;
            }

            p {
                text-align: justify;
                font-size: calc(25px + 0.5vw);
                padding: 15px 0;
            }
            .minting-screen {
                margin: 0 0 0 30px;
                font-size: 50px;
            }
        }
    }
}
.large-display {
    .minting-section {
        .minting-text-top {
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 20vh auto;
            grid-template-areas:
                " a b "
                " c c ";

            h2 {
                text-align: left;
                font-weight: bolder;
                font-size: 50px;
                padding: 60px 0 0;
            }
            h3 {
                text-align: left;
                font-size: 35px;
                padding: 10px 0 0 0;
                font-weight: normal;
            }

            p {
                text-align: justify;
                font-size: 30px;
                padding: 15px 0 0 0;
            }
            .minting-screen {
                margin: 0 0 0 50px;
                font-size: 60px;
            }
        }
    }
}

.minting-section {
    position: relative;
    .container {
        padding-top: 0;
    }
    .minting-text-top {
        display: grid;
        top: 0;
        left: 0;
        margin-top: -30px;

        h2 {
            text-align: left;
            font-weight: bolder;
            font-size: 30px;
            padding: 0 30px 0 30px;
        }
        h3 {
            text-align: left;
            font-size: x-large;
            padding: 0 30px 0 30px;
        }
    }
}
</style>