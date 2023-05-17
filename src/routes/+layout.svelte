<script>
	import '../app.css';
	import Navbar from '../lib/navbar.svelte';
	import { onMount } from 'svelte';
	let days = 0;
	let hours = 0;
	let minutes = 0;
	let sec = 0;
	onMount(() => {
		//new Date(year, monthIndex, day, hours, minutes)
		const target = new Date(2030, 0, 1, 0, 0);
		const updateTime = () => {
			const diff = target.getTime() - new Date().getTime();
			days = Math.floor(diff / 86400000);
			hours = Math.floor((diff - days * 86400000) / 3600000);
			minutes = Math.floor((diff - days * 86400000 - hours * 3600000) / 60000);
			sec = Math.floor((diff - days * 86400000 - hours * 3600000 - minutes * 60000) / 1000);
		};
		updateTime();
		setInterval(() => {
			updateTime();
		}, 1000);
	});
</script>

<main class="bg-[#665b49] min-h-screen h-full min-w-full pb-40">
	<Navbar />
	<slot />
    <!-- <div class="border-gray-50 text-white"> -->
    <!--     {days} Days -->
    <!--     {hours} Hours -->
    <!--     {minutes} Minutes -->
    <!--     {sec} Seconds -->
    <!-- </div> -->
</main>
