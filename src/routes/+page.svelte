<script>
	import AudioPlayer from "../components/AudioPlayer/AudioPlayer.svelte";
	import { tracks } from "../components/AudioPlayer/tracks";
	import Congratulations from "../components/Congratulations.svelte";
	import foto1 from "../lib/images/foto1.jpg";

	//const targetDate = new Date("2023-12-26T00:00:00"); // 26 de diciembre
	const targetDate = new Date("2023-12-22T17:30:30"); // 26 de diciembre

	let remainingTime = {};

	function updateRemainingTime() {
		const now = new Date();
		const nowHour = now.getHours();
		const targetHour = targetDate.getHours();

		const difference = targetDate - now;

		if (difference <= 0) {
			remainingTime = {
				days: 0,
				hours: 0,
				minutes: 0,
				seconds: 0,
			};
			return;
		}

		remainingTime = {
			days: Math.floor(difference / (1000 * 60 * 60 * 24)),
			hours: Math.floor(
				(difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60),
			),
			minutes: Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60)),
			seconds: Math.floor((difference % (1000 * 60)) / 1000),
		};
	}

	setInterval(updateRemainingTime, 1000);
	const formatter = new Intl.DateTimeFormat("en", {
		hour12: true,
		hour: "numeric",
		minute: "2-digit",
		second: "2-digit",
	});
</script>

<svelte:head>
	<title>Regalo Cristian</title>
	<meta name="description" content="Regalo Cristian" />
	<link
		href="https://fonts.googleapis.com/css2?family=Rubik+Lines&display=swap"
		rel="stylesheet"
	/>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap"
		rel="stylesheet"
	/>
</svelte:head>
<main>
	<div class="text-column">
		{#if remainingTime.days > 0 || remainingTime.hours > 0 || remainingTime.minutes > 0 || remainingTime.seconds > 0}
			<p>
				Tiempo hasta el 26 de diciembre (cumple de mi <strong
					>CRISTIAN</strong
				>):<br />
				<span class="clock">
					{remainingTime.days}
					días, {remainingTime.hours}
					horas, {remainingTime.minutes} minutos, {remainingTime.seconds}
					segundos</span
				>
			</p>
		{:else}
			{#each tracks as track}
				<AudioPlayer {...track} />
			{/each}
			<Congratulations />
			<figure class="wave">
				<img
					src="https://pedelriomarron.github.io/cumple_cristian/_app/immutable/assets/foto1.bOP47yIb.jpg"
					alt="amigos"
				/>
				<figcaption>Foto de amigos</figcaption>
			</figure>
			<footer>
				<p class="footer">
					Para mi amigo Cristian, como somos medio gitanos, no quiero
					gastarme mucho dinero, pero para que veas que me importas te
					muestro como dedico algo más valioso que el dinero, que es
					el tiempo en hacerte estas cositas en tu cumpleaños. Un
					abrazo
				</p>
			</footer>
		{/if}
	</div>
</main>

<style>
	.centered {
		display: flex;
		flex-direction: column;
		height: 100%;
		justify-content: center;
		gap: 0.5em;
		max-width: 40em;
		margin: 0 auto;
	}

	p {
		font-family: Dancing Script;
		font-size: 2em;
	}

	.clock {
		color: rgb(0, 0, 0);
		font-family: Rubik Lines;
		font-size: 1em;
	}

	.wave {
		float: left;
		margin: 20px;
		animation: wave ease-in-out 2.5s infinite alternate;
		transform-origin: center -36px;
	}

	.wave:hover {
		animation-play-state: paused;
		cursor: pointer;
	}

	.wave img {
		border: 5px solid #f8f8f8;
		display: block;
		width: 20em;
		height: 20em;
	}

	.wave figcaption {
		text-align: center;
	}

	.wave:after {
		content: "";
		position: absolute;
		width: 20px;
		height: 20px;
		border: 1.5px solid #ffffff;
		top: -10px;
		left: 50%;
		border-bottom: none;
		border-right: none;
		transform: rotate(35deg);
	}

	.wave:before {
		content: "";
		position: absolute;
		top: -23px;
		left: 50%;
		display: block;
		height: 44px;
		width: 47px;
		background-size: 20px 20px;
		background-repeat: no-repeat;
		z-index: 16;
	}

	@keyframes wave {
		0% {
			transform: rotate(10deg);
		}
		100% {
			transform: rotate(-10deg);
		}
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding-left: 100px;
		padding-right: 100px;
	}

	footer a {
		font-weight: bold;
	}
</style>
