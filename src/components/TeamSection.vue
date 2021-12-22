<template>
    <section class="team-section">
        <div class="container">
            <div class="team">
                <h2>The Team</h2>
                <!-- <h3>What's a KID?</h3> -->
                <p>
                    Every <span class="important">cool project</span> has a cool
                    team behind. In our case, our team is the coolest posible
                    mixture of kickassness.
                </p>
                <div class="profile-cards">
                    <div class="profile-card">
                        <img
                            class="figure"
                            src="../assets/demon_kid.jpg"
                            alt=""
                        />
                        <div href="" class="team-member-data">
                            <h3 class="team-member-name">
                                ultra <br class="small-spuff" />Kelevra
                            </h3>
                            <p class="team-member-role">Creative Goblin</p>
                            <a href="https://twitter.com/ultraKelevra"
                                >@ultraKelevra</a
                            >
                        </div>
                    </div>

                    <div class="profile-card">
                        <img
                            class="figure"
                            src="../assets/whale_kid.jpg"
                            alt=""
                        />
                        <div href="" class="team-member-data">
                            <h3 class="team-member-name">
                                Arsubanipal <br class="small-spuff" />666
                            </h3>
                            <p class="team-member-role">Whale Wannabe</p>
                            <a href="https://twitter.com/arsubanipal666"
                                >@arsubanipal666</a
                            >
                        </div>
                    </div>

                    <div class="profile-card">
                        <img
                            class="figure"
                            src="../assets/blue_kid.jpg"
                            alt=""
                        />
                        <div href="" class="team-member-data">
                            <h3 class="team-member-name">
                                Ernesto <br class="small-spuff" />Cisneros
                            </h3>
                            <p class="team-member-role">Charisma Demon</p>
                            <a href="https://twitter.com/ErnestCisneros1"
                                >@ErnestCisneros1</a
                            >
                        </div>
                    </div>
                    <div class="profile-card">
                        <img
                            class="figure"
                            src="../assets/monke_pfp.jpg"
                            alt=""
                        />
                        <div href="" class="team-member-data">
                            <h3 class="team-member-name">
                                Gianni <br class="small-spuff" />Dalerta
                            </h3>
                            <p class="team-member-role">Old Wise Ape</p>
                            <a href="https://twitter.com/GianniDalerta"
                                >@GianniDalerta</a
                            >
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {};
    },
};
</script>

<style lang=scss>
.team-section {
    .team {
        .profile-cards {
            padding-top: 50px;
            display: grid;
            grid-gap: 25px;
            .profile-card {
                position: relative;
                width: 100%;
                display: flex;
                flex-direction: column;
                justify-content: flex-start;
                align-items: stretch;
                img {
                    width: 100%;
                    border-radius: 15px;
                }
                .team-member-data {
                    text-decoration: none;
                    .team-member-role,
                    .team-member-name {
                        padding: 0;
                    }
                    .team-member-name {
                    }
                    .team-member-role {
                    }
                    a {
                        width: 100%;
                        background: url("../assets/twitter-logo-white.svg");
                        background-repeat: no-repeat;
                        height: 35px;
                        display: block;
                        margin-top: 15px;
                        font-size: x-large;
                        font-family: "rubik-regular";
                        text-align: left;
                        padding-left: 55px;
                        color: #7990ff;
                    }
                }
            }
        }
    }
}
.small-display {
    .team {
        .profile-cards {
            color: white;

            .profile-card {
                color: white;
                padding: 0 0 25px 0;
                img {
                    width: calc(100vw - 60px);
                    margin-left: 30px;
                }
                .team-member-data {
                    padding: 0 30px;
                    text-decoration: none;
                    .team-member-role,
                    .team-member-name {
                        padding: 0;
                        font-size: 20px;
                    }
                    .team-member-name {
                        margin: 0;
                        font-size: 35px;
                    }
                    .team-member-role {
                        margin: 0;
                        font-size: 25px;
                    }
                    a {
                        height: 35px;
                        display: block;
                        margin-top: 15px;
                        text-align: left;
                    }
                }
            }
        }
    }
}
.small-horizontal-display {
    .team {
        .profile-cards {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr;
            position: relative;
            width: 100%;

            .profile-card {
                color: white;

                img {
                    border-radius: 15px;
                }
                h3 {
                    color: white;
                }
                a {
                    color: white;
                }
            }
        }
    }
}
.med-display {
    .team {
        .profile-cards {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr;
            position: relative;
            width: 100%;

            .profile-card {
                color: white;

                img {
                    border-radius: 15px;
                }
                h3 {
                    color: white;
                }
                a {
                    color: white;
                }
            }
        }
    }
}
.large-display {
    .team {
        .profile-cards {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr;
            position: relative;
            width: 100%;
            .profile-card {
                img {
                    border-radius: 15px;
                }
                h3 {
                    color: white;
                }
                a {
                    color: white;
                }
            }
        }
    }
}
</style>