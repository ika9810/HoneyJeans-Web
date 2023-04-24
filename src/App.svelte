<script>
  import { onMount } from "svelte";

	import Search from "./Search.svelte";
	import CardList from "./Cards.svelte";
	import Card from "./lib/components/CardProxy.svelte";

	let showcase, basics, reverse, holos, cosmos, amazings, radiant, basicGallery, 
			vee, veeUltra, veeAlt, veeMax, veeMaxAlt, veeStar, 
			trainerHolo, rainbow, gold, veeGallery, shinyVault;

	let query = "";
	let isLoading = true;

	const getCards = async () => {
		let promiseArray = [];
		let cardFetch = await fetch("/data/cards.json");
		let cards = await cardFetch.json();
		return cards;
	};

	const loadCards = async() => {
		return getCards()
			.then((cards) => {
				// @ts-ignore
				window.cards = cards;
				showcase = cards[0];
				basics = cards.slice(1, 4);
				reverse = [...cards.slice(4, 7), ...cards.slice(70,76)];
				holos = cards.slice(7, 13);
				cosmos = cards.slice(13, 16);
				amazings = cards.slice(76, 85);
				radiant = cards.slice(16, 19);
				basicGallery = cards.slice(19, 22);
				vee = cards.slice(22, 25);
				veeUltra = cards.slice(25, 28);
				veeAlt = cards.slice(28, 34);
				veeMax = cards.slice(37, 40);
				veeMaxAlt = cards.slice(40, 43);
				veeStar = cards.slice(43, 46);
				trainerHolo = cards.slice(46, 52);
				rainbow = cards.slice(52, 58);
				gold = cards.slice(58, 64);
				veeGallery = cards.slice(64, 70);
				shinyVault = cards.slice(85,91);
				isLoading = false;
			});
	};

	onMount(() => {
		loadCards();
		const $headings = document.querySelectorAll("h1,h2,h3");
		const $anchor = [...$headings].filter((el) => {
			const id = el.getAttribute("id")?.replace(/^.*?-/g,"");
			const hash = window.location.hash?.replace(/^.*?-/g,"")
			return id === hash;
		})[0];
		if( $anchor ) {
			setTimeout(() => {
				$anchor.scrollIntoView();
			},100);
		}
	});
</script>

<main>
	<header>
		<h1 id="⚓-top">HoneyJeans</h1>

		<p class="author">By 
			<em><a href="https://github.com/ika9810/Honey-Jeans"><svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><title>GitHub</title><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>HoneyJeans</em>
		</p>
		
		<section class="intro" id="⚓-intro">
			<p>
				🌈 Welcome to HoneyJeans! 🌈 <br>
				🐰 Featuring NewJeans' Official Character, "Tokki" 🎉<br>
				🔥 Uniquely generated & stylishly curated memes 👩‍🎨<br>
				⌛ Get the latest HoneyJeans Memes every 8 hours! 🔄
				<!-- <mark>HoneyJeans</mark> is a collection of randomly generated and stylistically curated Memes based on NewJeans Official Character, <mark>"Tokki"</mark>
				A collection of <mark>advanced CSS</mark> styles to create
				<mark>realistic-looking effects</mark> for the faces of Pokemon cards. 
				The cards use <mark>3d transforms</mark>, <mark>filters</mark>, <mark>blend modes</mark>,
				<mark>css gradients</mark> and interactions to provide a unique experience when taking a closer look! -->
			</p>
		</section>

		<div class="showcase">
			{#if !showcase}
				loading...
			{:else}
				<Card
					id={showcase.id}
					name={showcase.name}
					set={showcase.set}
					number={showcase.number}
					types={showcase.types}
					supertype={showcase.supertype}
					subtypes={showcase.subtypes}
					rarity={showcase.rarity}
					isReverse={showcase.isReverse}
					showcase={true}
				/>
			{/if}
		</div>

		<section class="info">
			<!-- <h2>Click on a Card to take a Closer look!</h2> -->

			<hr />

			<p class="small">
				<strong>⏰ HoneyJeans Daily Meme is updated every 8 hours! </strong>
					<br>
					🚨 The assets and all files generated from this page are NOT commercially available. <br>
					<a href="https://raw.githubusercontent.com/ika9810/Honey-Jeans/main/build/images/1.png" target ='_blank'>👊 Click Here to Download HoneyJeans Meme Image! 🐇</a><br><br>
					<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fhoneyjeans.honeyvuitton.com&count_bg=%235A699D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false"/></a>
			</p>
		</section>
	</header>		
</main>
