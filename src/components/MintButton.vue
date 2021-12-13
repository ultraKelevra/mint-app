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

export default {
	data() {
		return {
			displayMintMenu: true,
			connecting: false,
			contractAddress: "1234567890",
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
				gatheredData: true,
				kidzBalance: 0,
				kidzPerWallet: 10,
				limited: true,
			},
		};
	},
	computed: {
		mintButtonDisabled() {
			return (
				this.kidzToMint == 0 ||
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
				if (this.kidzData.gatheredData)
					if (this.kidzData.limited)
						return (
							"Your wallet currently has <span class='important'>" +
							this.kidzData.kidzBalance +
							" kidz </span>. The current limit per wallet is <span class='important'>" +
							this.kidzData.kidzPerWallet +
							" kidz</span>. You can mint up to <span class='important'>" +
							(this.kidzData.kidzPerWallet -
								this.kidzData.kidzBalance) +
							" kidz</span>."
						);
					else
						return "There is currently no limit to how many kidz you can mint :D";
				else return "Gathering your kid balance information";
			}
			return "Connect your <span class=important>METAMASK</span> wallet to get started :)";
		},
	},
	methods: {
		kidsToMintButtonActionUp() {
			this.kidzToMint++;
			this.checkKidzAmount();
		},
		kidsToMintButtonActionDown() {
			this.kidzToMint--;
			this.checkKidzAmount();
		},
		closeMenu() {
			if (!this.interactable) return;
			this.displayMintMenu = false;
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
			if (!this.interactable) return;

			console.log("minting: " + this.kidzToMint + " kidz");
		},
		reset() {
			this.kidzToMint = 1;
			this.walletData.connected = false;
			this.walletData.rejectedConnection = false;
			this.kidzData.gatheredData = false;
			this.walletData.availableProvider = false;
		},
		connectButton() {
			if (!this.interactable) return;

			if (this.kidzToMint <= 0) return;
			if (this.walletData.connected) {
				this.mint();
			} else {
				this.connect();
			}
		},
		instantiateContract() {},
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
						},
						() => {
							self.walletData.rejectedConnection = true;
							self.disabled = false;
							self.connecting = false;
						}
					);
					// p.on("connect", () => console.log("connected"));
					// p.on("disconnect", () => console.log("disconnected"));
					p.on("accountsChanged", () => {
						self.walletData.rejectedConnection = true;
						self.disabled = false;
						self.connecting = false;
						self.walletData.connected = false;
					});
					// p.on("chainChanged", () => console.log("chain changed"));
				},
				() => {
					self.disabled = false;
					self.walletData.availableProvider = false;
				}
			);
		},
	},
};
</script>

<style lang="scss">
.mint-screen-container.deployed {
	height: 85vh;
}
.mint-screen-container:not(.deployed) {
	height: 100%;
}
.mint-menu-enter-active {
}
.mint-menu-leave-active {
}
.small-display .mint-screen-container {
}
.small-horizontal-display .mint-screen-container {
}
.med-display .mint-screen-container {
}

.large-display .mint-screen-container {
	height: 80vh;
	width: 100%;
	bottom: 0;
	right: 0;
	padding: 0;
	align-items: center;
	grid-template-columns: 1fr;
	grid-template-rows: 50px 1fr 1fr 20vh;
	p {
		padding-top: 50px !important;
	}
	.minting-form {
		display: flex;
		flex-direction: column;
		align-content: center;
		justify-content: center;
		align-items: stretch;
		input {
			height: 80px;
			font-size: 40px;
			padding: 0 40px;
		}
	}
}
.deployed {
	.minting-screen {
		button {
			.graphics-container {
			}
		}
	}
}
.minting-screen {
	label {
		&.disabled {
			color: gray;
		}
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
		transition: 0.15s;
		transform: scale(1);

		&:hover {
			transform: scale(0.8);
		}
	}
	.mint-screen-container {
		position: absolute;
		z-index: -1;
		display: grid;
		box-sizing: border-box;

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
			filter: drop-shadow(0 0 25pxpx rgba(255, 217, 0, 0));
			transform-origin: center;
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