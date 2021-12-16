<template>
    <div class="minting-screen">
        <div
            class="mint-screen-container"
            :class="{ deployed: displayMintMenu }"
        >
            <div class="mint-screen-background"></div>
            <div class="cross-icon" @click="closeMenu"></div>
            <p v-html="descriptionText"></p>
            <form class="minting-form">
                <label
                    for="#amountToMint"
                    class="gold"
                    :class="{ disabled: mintAmountDisabled }"
                    >Mint Amount</label
                >
                <div class="input-container">
                    <input
                        id="amountToMint"
                        type="number"
                        :disabled="mintAmountDisabled"
                        v-model.number="kidzToMint"
                        @change="checkKidzAmount"
                    />
                    <div
                        class="number-input-up"
                        :class="{ disabled: mintAmountDisabled }"
                        @click="kidsToMintButtonActionUp"
                    >
                        v
                    </div>
                    <div
                        class="number-input-down"
                        :class="{ disabled: mintAmountDisabled }"
                        @click="kidsToMintButtonActionDown"
                    >
                        v
                    </div>
                </div>
            </form>
        </div>

        <button
            style="grid-area: b"
            id="about"
            @click="connectButton"
            :disabled="mintButtonDisabled"
            :class="{ galaxy: walletData.connected && !mintButtonDisabled }"
        >
            <div class="graphics-container">
                <div class="button-background-0"></div>
                <div class="button-background-1"></div>
            </div>
            <span>{{ buttonText }}</span>
        </button>
    </div>
</template>

<script>
import Web3 from "web3";
import getProvider from "@metamask/detect-provider";
import eventBus from "../eventBus";
import contract from "../smartContract/smart_contract_interface";

export default {
    data() {
        return {
            contractInstance: null,
            displayMintMenu: false,
            connecting: false,
            networdId: 2,
            kidzToMint: 1,
            interactable: true,
            walletData: {
                web3: null,
                address: "",
                networkId: null,
                availableProvider: false,
                rejectedConnection: false,
                connected: false,
            },
            kidzData: {
                gatheredData: false,
                kidzBalance: 0,
                kidzPerWallet: 10,
                limited: true,
                kidNumber: 0,
                kidPrice: 0,
            },
        };
    },
    computed: {
        mintButtonDisabled() {
            return (
                (this.walletData.connected && this.kidzToMint == 0) ||
                (this.walletData.connected && !this.kidzData.gatheredData)
            );
        },
        mintAmountDisabled() {
            return !this.walletData.connected || !this.kidzData.gatheredData;
        },
        buttonText() {
            if (
                this.connecting ||
                (this.walletData.connected && !this.kidzData.gatheredData)
            )
                return "...";
            if (this.walletData.connected) return "MINT";
            return "CONNECT WALLET";
        },

        descriptionText() {
            if (this.connecting)
                return "connecting... check your metamask tab or popup.";
            if (this.walletData.connected) {
                if (this.kidzData.gatheredData) {
                    console.log("top description = " + this.topDescription());
                    return (
                        this.topDescription() +
                        "<br />" +
                        (this.kidzToMint > 0 ? this.priceDescription() : "")
                    );
                } else return "Gathering your kid balance information";
            }
            return "Connect your <span class=important>METAMASK</span> wallet to get started :)";
        },
    },
    methods: {
        topDescription() {
            return this.kidzData.limited
                ? "Your wallet currently has <span class='important'>" +
                      this.kidzData.kidzBalance +
                      " kidz </span>. The current limit per wallet is <span class='important'>" +
                      this.kidzData.kidzPerWallet +
                      " kidz</span>. You can mint up to <span class='important'>" +
                      (this.kidzData.kidzPerWallet -
                          this.kidzData.kidzBalance) +
                      " kidz</span>.<br />"
                : "There is currently no limit to how many kidz you can mint :D<br />";
        },
        priceDescription() {
            var kidAmount = this.kidzToMint;
            var price = (
                Math.round(
                    this.walletData.web3.utils.fromWei(
                        this.kidzData.kidPrice,
                        "ether"
                    ) *
                        kidAmount *
                        100
                ) / 100
            ).toString();
            return (
                "The price of <span class='important'>" +
                (kidAmount > 1 ? this.kidzToMint + " kidz" : "a kid") +
                "</span> is:<br /><span class='gold' style='font-family: rubik'>" +
                price +
                " ether</span>."
            );
        },
        kidsToMintButtonActionUp() {
            if (this.mintAmountDisabled) return;
            this.kidzToMint++;
            this.checkKidzAmount();
        },
        kidsToMintButtonActionDown() {
            if (this.mintAmountDisabled) return;
            this.kidzToMint--;
            this.checkKidzAmount();
        },
        closeMenu() {
            if (!this.interactable) return;
            this.reset();
        },
        checkKidzAmount() {
            if (this.kidzData.limited) {
                var kidzPerWallet = this.kidzData.kidzPerWallet;
                var kidzBalance = this.kidzData.kidzBalance;
                var allowedKidz = kidzPerWallet - kidzBalance;
                this.kidzToMint = Math.min(this.kidzToMint, allowedKidz);
            }
            if (this.kidzToMint < 0)
                this.kidzToMint = this.allowedKidz > 0 ? 1 : 0;
        },

        mint() {
            if (!this.interactable) {
                return;
            }
            if (!this.kidzToMint > 0) return;
            this.contractInstance.methods.mint(this.kidzToMint).send({
                from: this.walletData.address,
                value: this.kidzData.kidPrice * this.kidzToMint,
            });
        },
        reset() {
            this.kidzToMint = 1;
            this.walletData.connected = false;
            this.walletData.rejectedConnection = false;
            this.kidzData.gatheredData = false;
            this.walletData.availableProvider = false;
            this.displayMintMenu = false;
        },
        connectButton() {
            if (!this.interactable) return;
            console.log("button is interactable");
            if (this.walletData.connected) {
                console.log("button says minting");
                this.mint();
            } else {
                console.log("button is connecting");
                this.displayMintMenu = true;
                this.connect();
            }
        },
        instantiateContract() {
            console.log(contract.address);
            console.log(contract.abi);

            this.contractInstance = new this.walletData.web3.eth.Contract(
                contract.abi,
                contract.address
            );
        },
        updateKidData() {
            this.interactable = false;
            var self = this;
            this.contractInstance.methods
                .totalSupply()
                .call()
                .then((n) => (self.kidzData.kidNumber = n));
            this.contractInstance.methods
                .balanceOf(this.walletData.address)
                .call()
                .then((n) => (self.kidzData.kidzBalance = n));
            this.contractInstance.methods
                .maxTokensPerWallet()
                .call()
                .then((n) => {
                    self.interactable = true;
                    self.kidzData.kidzPerWallet = n;
                    console.log("current max kidz per wallet is: " + n);
                    self.kidzData.limited = n ? true : false;
                });
            this.contractInstance.methods
                .price()
                .call()
                .then((n) => {
                    console.log("data gathered");
                    self.kidzData.kidPrice = n;
                    self.kidzData.gatheredData = true;
                });
        },
        connect() {
            var walletData = this.walletData;
            this.disabled = true;
            this.walletData.web3 = null;
            this.walletData.address = "";

            this.walletData.networkId = null;
            this.walletData.availableProvider = true;
            this.walletData.rejectedConnection = false;
            this.walletData.connected = false;
            this.connecting = true;

            var self = this;
            getProvider().then(
                (p) => {
                    p.enable().then(
                        (accounts) => {
                            let web3 = new Web3(p);
                            web3.eth.net
                                .getId()
                                .then((id) => (walletData.networkId = id));
                            self.walletData.web3 = web3;

                            self.walletData.connected = true;
                            self.walletData.address = accounts[0];
                            self.disabled = false;
                            self.connecting = false;
                            self.instantiateContract();
                            self.updateKidData();
                            console.log("gathering data right now");
                            // p.on("accountsChanged", () => self.reset());
                            // p.on("networkChanged", () => self.reset());
                        },
                        () => {
                            self.walletData.rejectedConnection = true;
                            self.disabled = false;
                            self.connecting = false;
                        }
                    );
                    p.on("accountsChanged", () => {
                        self.walletData.rejectedConnection = true;
                        self.disabled = false;
                        self.connecting = false;
                        self.walletData.connected = false;
                    });
                },
                () => {
                    self.disabled = false;
                    self.walletData.availableProvider = false;
                }
            );
        },
    },
    mounted() {
        var self = this;
        eventBus.$on("open-mint-menu", () => {
            self.displayMintMenu = true;
        });
    },
    beforeUnmount() {
        eventBus.$off("open-mint-menu");
    },
};
</script>

<style lang="scss">
.large-display {
    .mint-screen-container {
        width: 100%;
        bottom: 0;
        right: 0;
        padding: 0;
        align-items: center;
        grid-template-columns: 1fr;
        grid-template-rows: 50px 1fr 1fr 20vh;
        grid-template-areas:
            "t"
            "a"
            "b";
        p {
            padding-top: 50px !important;
        }
        .minting-form {
            display: flex;
            flex-direction: column;
            align-content: center;
            justify-content: center;
            align-items: stretch;
            grid-area: b;
            input {
                height: 80px;
                font-size: 40px;
                padding: 0 40px;
            }
        }
        &.deployed {
            height: 80vh;
            opacity: 1;
        }
        &:not(.deployed) {
            overflow: hidden;
            height: 20vh;
        }
    }
}
.med-display {
    .mint-screen-container {
        // height: 80vh;
        bottom: 0;
        right: 0;
        padding: 0;
        align-items: center;
        grid-template-columns: 1fr 1fr;
        grid-template-areas:
            "a t"
            "a b"
            "a .";
        grid-template-rows: 50px 1fr 20vh;
        grid-gap: 0 60px;
        p {
            padding-top: 50px !important;
        }
        .minting-form {
            input {
                height: 80px;
                font-size: 40px;
                padding: 0 40px;
            }
        }
        .mint-screen-background {
            left: -15px;
            right: -15px;
            bottom: -15px;
            top: -15px;
        }

        &.deployed {
            height: 80vh;
            opacity: 1;
            width: calc(100vw - 100px);
        }
        &:not(.deployed) {
            overflow: hidden;
            height: 20vh;
            width: calc((100vw - 160px) / 2);
        }
    }
}

.small-horizontal-display {
    .minting-screen {
        .mint-screen-container {
            bottom: 0;
            right: 0;
            padding: 0;
            align-items: center;
            grid-template-columns: 1fr 1fr;
            grid-template-areas:
                "a t"
                "a b"
                "a .";
            grid-template-rows: 50px 1fr 20vh;
            grid-gap: 0 60px;
            button {
                span {
                    font-size: 25px;
                }
            }
            &.deployed {
                height: 75vh;
                opacity: 1;
                width: calc(100vw - 160px);
                .mint-screen-background {
                    left: -10px;
                    right: -10px;
                    bottom: -10px;
                    top: -10px;
                }
            }
            &:not(.deployed) {
                height: 20vh;
                width: 100%;
            }

            .minting-form {
                input {
                    height: 60px;
                    font-size: 30px;
                    padding: 0 30px;
                }
                .number-input-up,
                .number-input-down {
                    width: 60px;
                    height: 60px;
                    font-size: 43px;
                }
                .number-input-up {
                    right: 60px;
                }
            }
        }
    }
}
.small-display {
    .mint-screen-container {
        width: 100%;
        bottom: 0;
        right: 0;
        padding: 0;
        align-items: center;
        grid-template-columns: 1fr;
        grid-template-rows: 50px 1fr 1fr 20vh;
        grid-template-areas:
            "t"
            "a"
            "b";
        p {
            padding: 0 !important;
        }
        .minting-form {
            display: flex;
            flex-direction: column;
            align-content: center;
            justify-content: center;
            align-items: stretch;
            grid-area: b;
            input {
                height: 80px;
                font-size: 40px;
                padding: 0 40px;
            }
            .number-input-down,
            .number-input-up {
                font-size: 60px;
            }
        }
        &.deployed {
            height: 80vh;
            opacity: 1;
        }
        &:not(.deployed) {
            overflow: hidden;
            height: 15vh;
        }
    }
}

.minting-screen {
    label {
        &.disabled {
            color: gray;
        }
    }
    form {
        display: flex;
        flex-direction: column;
    }
    input {
        background: #4a356b;
        border: 1px solid gold;
        border-radius: 15px;
        height: 80px;
        font-size: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 0 40px;
        color: gold;
        font-family: "rubik";
        appearance: textfield;
        transition: 0.15s;
        &:disabled {
            color: gray;
            border: 1px solid gray;
            background: rgb(0, 0, 0);
            &:hover {
                color: gray;
                background: rgb(30, 30, 30);

                border: 1px solid gray;
            }
        }
    }
    .input-container {
        grid-area: b;
        position: relative;
        display: flex;
        align-items: center;
        align-content: center;
        justify-content: space-between;
        flex-direction: row;
        grid-gap: 5px;
        .number-input-up,
        .number-input-down {
            user-select: none;
            cursor: pointer;
            position: absolute;
            width: 80px;
            height: 80px;
            border: none;
            right: 0;
            transition: 0.15s;
            &:hover:not(.disabled) {
                background: rgb(173, 139, 195);
                color: rgb(255, 255, 255);
            }
            &:disabled {
                color: gray;
                border: 1px solid gray;
                background: rgb(0, 0, 0);
                &:hover {
                    color: gray;
                    background: rgb(30, 30, 30);

                    border: 1px solid gray;
                }
            }
        }
        .number-input-up {
            right: 80px;
            transform: scale(1, -1);
            border-radius: 15px 0 0 15px;
            border-left: 1px solid gold;
            &.disabled {
                border-color: gray;
            }
        }
        .number-input-down {
            border-radius: 0 15px 15px 0;
        }
    }
    .cross-icon {
        cursor: pointer;
        grid-area: t;
        margin-top: 15px;
        right: 0;
        width: 35px;
        height: 35px;
        bottom: 0;
        background-position: center;
        background-repeat: no-repeat;
        background-size: contain;
        background-origin: 50% 50%;
        background-image: url("../assets/icons/cross.svg");
        justify-self: flex-end;
    }
    .mint-screen-container {
        position: absolute;
        z-index: -1;
        display: grid;
        box-sizing: border-box;
        transition: height 0.5s, width 0.5s, opacity 0.75s;
        p {
            grid-area: a;
        }
        .mint-screen-background {
            background: black;
            border: 1px solid gold;
            border-radius: 15px;
            position: absolute;
            left: -15px;
            right: -15px;
            bottom: -15px;
            top: -15px;
            box-sizing: border-box;
            z-index: -1;
            transition: 0.15s 0.25s;
        }
        > * {
            transition: opacity 0.15s;
        }
        &.deployed {
            opacity: 1;
        }
        &:not(.deployed) {
            overflow: hidden;

            .mint-screen-background {
                left: 0;
                right: 0;
                bottom: 0;
                top: 0;
                width: unset;
                height: unset;
            }
            > *:not(.mint-screen-background) {
                opacity: 0;
            }
        }
    }

    font-family: "rubik";
    margin: 0 30px 0 30px;
    transform: translateY(-5vh);

    button {
        overflow: hidden;
        width: 100%;
        height: 100%;
        border-radius: 15px;
        border: solid 1px gold;
        background: black;
        color: gold;
        box-sizing: border-box;
        font-weight: bolder;
        font-size: xx-large;
        transition: border-width 0.25s, background-color 0.15s;
        font-family: "rubik";
        span {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            transition: 0.5s;
            filter: drop-shadow(0 0 25px rgba(255, 217, 0, 0));
            transform-origin: center;
            width: calc(100% - 60px);
        }
        .graphics-container {
            overflow: hidden;
            position: absolute;
            border: 1px solid gold;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            border-radius: 15px;
            transition: 2s;
            opacity: 0;
        }
        .button-background-0 {
            top: -12.5%;
            left: -12.5%;
            position: absolute;
            width: 125%;
            height: 125%;
            background-size: cover;
            background-image: url("../assets/starmap/starmap_tall_bg.svg");
            background-position: center;
            transform: scale(calc(1 / 1.25));
            transition: 0.5s;
            transform-origin: center;
            opacity: 0.75;
        }
        .button-background-1 {
            top: -25%;
            left: -25%;
            position: absolute;
            width: 150%;
            height: 150%;
            background-size: cover;
            background-image: url("../assets/starmap/stars.svg");
            background-position: center;
            transform: scale(calc(1 / 1.5));
            transition: 0.5s;
            position: 50%;
            transform-origin: center;
        }
        &.galaxy {
            background: black;
            .graphics-container {
                opacity: 0.5;
            }
            .button-background-0 {
                transform: scale(calc(1 / 1.25));
            }
            .button-background-1 {
                transform: scale(calc(1 / 1.5));
            }
            &:hover {
                .graphics-container {
                    opacity: 1;
                }
                .button-background-0 {
                    opacity: 0.3;
                    transform: scale(1);
                }
                .button-background-1 {
                    transform: scale(1);
                    opacity: 1;
                    filter: drop-shadow(0 0 5px gold);
                }
                span {
                    transform: translate(-50%, -50%) scale(1.3);
                    filter: drop-shadow(0 0 25px gold);
                }
            }
        }

        &:hover:not(.galaxy) {
            color: black;
            background: gold;
            border-color: black;
            // border-width: 3px;
            // border-radius: 25px;
            span {
                transform: translate(-50%, -50%) scale(0.85);
            }
        }
        &:disabled {
            .graphics-container {
                opacity: 0;
            }
            .button-background-0 {
                transform: scale(1);
            }
            .button-background-1 {
                transform: scale(1);
            }
            color: gray;
            border: 1px solid gray;
            border-radius: 15px;
            .button-background-0 {
                opacity: 0;
            }
            .button-background-1 {
                opacity: 0;
            }
            &:hover {
                color: gray;
                background: rgb(30, 30, 30);
                border: 1px solid gray;
                span {
                    transform: translate(-50%, -50%);
                }
            }
        }
    }
}
</style>