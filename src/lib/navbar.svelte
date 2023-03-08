<script>
    import { page } from '$app/stores';
    import { onMount, onDestroy } from "svelte";
    import { browser } from '$app/environment';
    const MOBILE_WIDTH = 800;
    let mobile = false;
    if (browser) {
        const handleResize = (e) => {
            mobile = innerWidth < MOBILE_WIDTH;
        }
        handleResize();
        window.addEventListener("resize", handleResize)
        const debounce = (fn, interval) => {
            let timer;
            return function debounced(...args) {
                clearTimeout(timer);
                timer = setTimeout(function call() {
                    fn(...args);
                }, interval);
            };
        };
        onDestroy(() => {
            window.removeEventListener("scroll", handleResize);
        })
    }
    onMount(() => {
        let mobile = innerWidth < MOBILE_WIDTH;
    })
    let menuOpen = false;
</script>

<main>
    {#if mobile}
        <img class="p-2 h-20" src="/treeforce_logo.png" alt="" />
         <div class="text-[16px] inline m-4 content-center">
            <div class="navbar">
                <div class="container nav-container mb-10">
                    <input
                        bind:checked={menuOpen}
                        class="checkbox"
                        type="checkbox"
                        name=""
                        id=""
                    />
                    <div class="hamburger-lines">
                        <span class="line line1" />
                        <span class="line line2" />
                        <span class="line line3" />
                    </div>
                    <div class="menu-items rounded-md text-white text-lg">
                        {#if $page.url.pathname === '/'}
                            <a class="mt-6 text-[#BFDFED]" href="/" >about</a>
                        {:else}
                            <a on:click={() => menuOpen = false} class="mt-6 hover:text-[#BFDFED]" href="/" >about</a>
                        {/if}
                        {#if $page.url.pathname === '/blog'}
                            <a class="mt-6 text-[#BFDFED]" href="/blog" >blog</a>
                        {:else}
                            <a on:click={() => menuOpen = false} class="mt-6 hover:text-[#BFDFED]" href="/blog" >blog</a>
                        {/if}
                        {#if $page.url.pathname === '/team'}
                            <a class="mt-6 text-[#BFDFED]" href="/team" >our team</a>
                        {:else}
                            <a on:click={() => menuOpen = false} class="mt-6 hover:text-[#BFDFED]" href="/team" >our team</a>
                        {/if}
                        {#if $page.url.pathname === '/research'}
                            <a class="mt-6 text-[#BFDFED]" href="/research" >research</a>
                        {:else}
                            <a on:click={() => menuOpen = false} class="mt-6 hover:text-[#BFDFED]" href="/research" >research</a>
                        {/if}
                        {#if $page.url.pathname === '/contact'}
                            <a class="mt-6 text-[#BFDFED]" href="/contact" >contact us</a>
                        {:else}
                            <a on:click={() => menuOpen = false} class="mt-6 hover:text-[#BFDFED]" href="/contact" >contact us</a>
                        {/if}
                    </div>
                </div>
            </div>
        </div>
    {:else}
	<div class="p-[1%] flex font-bold">
		<img class="h-20" src="/treeforce_logo.png" alt="" />
        <ul class="flex ml-8 text-2xl bg-[#a08771] text-[#ede4df] w-full navbar">
            {#if $page.url.pathname === '/'}
                <a class="mt-6 text-[#BFDFED]" href="/" >about</a>
            {:else}
                <a class="mt-6 hover:text-[#BFDFED]" href="/" >about</a>
            {/if}
            {#if $page.url.pathname === '/blog'}
                <a class="mt-6 text-[#BFDFED]" href="/blog" >blog</a>
            {:else}
                <a class="mt-6 hover:text-[#BFDFED]" href="/blog" >blog</a>
            {/if}
            {#if $page.url.pathname === '/team'}
                <a class="mt-6 text-[#BFDFED]" href="/team" >our team</a>
            {:else}
                <a class="mt-6 hover:text-[#BFDFED]" href="/team" >our team</a>
            {/if}
            {#if $page.url.pathname === '/research'}
                <a class="mt-6 text-[#BFDFED]" href="/research" >research</a>
            {:else}
                <a class="mt-6 hover:text-[#BFDFED]" href="/research" >research</a>
            {/if}
            {#if $page.url.pathname === '/contact'}
                <a class="mt-6 text-[#BFDFED]" href="/contact" >contact us</a>
            {:else}
                <a class="mt-6 hover:text-[#BFDFED]" href="/contact" >contact us</a>
            {/if}
        </ul>
	</div>
    {/if}
</main>

<style>
.navbar {
    justify-content: space-around;
}
.nav-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.navbar .menu-items {
    z-index: 10;
    display: flex;
}
.navbar .nav-container li {
    list-style: none;
}
.navbar .nav-container a {
    padding: 0.7rem;
}
.nav-container {
    display: block;
}
.nav-container .checkbox {
    position: absolute;
    right: 20px;
    display: block;
    height: 32px;
    width: 32px;
    top: 20px;
    z-index: 500;
    opacity: 0;
    cursor: pointer;
}
.nav-container .hamburger-lines {
    display: block;
    height: 26px;
    width: 32px;
    position: absolute;
    top: 17px;
    right: 20px;
    z-index: 2;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.nav-container .hamburger-lines .line {
    display: block;
    height: 4px;
    width: 100%;
    border-radius: 10px;
    background: #fff;
}
.nav-container .hamburger-lines .line1 {
    transform-origin: 0% 0%;
    transition: transform 0.4s ease-in-out;
}
.nav-container .hamburger-lines .line2 {
    transition: transform 0.2s ease-in-out;
}
.nav-container .hamburger-lines .line3 {
    transform-origin: 0% 100%;
    transition: transform 0.4s ease-in-out;
}
.navbar .menu-items {
    box-shadow: inset 00 2000px rgba(160, 135, 113, 0.8);
    margin-top: 20px;
    height: fit-content;
    width: 50%;
    transform: translate(-150%);
    display: flex;
    flex-direction: column;
    transition: transform 0.3s ease-in-out;
    text-align: center;
    position: fixed;
    margin-right: 0px;
}
.navbar .menu-items li {
    margin-bottom: 1.2rem;
}
.logo {
    position: absolute;
    top: 5px;
    right: 15px;
    color: #fff;
}
.nav-container input[type="checkbox"]:checked ~ .menu-items {
    transform: translateX(0);
}
.nav-container input[type="checkbox"]:checked ~ .hamburger-lines .line1 {
    transform: rotate(45deg);
}
.nav-container input[type="checkbox"]:checked ~ .hamburger-lines .line2 {
    transform: scaleY(0);
}
.nav-container input[type="checkbox"]:checked ~ .hamburger-lines .line3 {
    transform: rotate(-45deg);
}
.nav-container input[type="checkbox"]:checked ~ .logo {
    display: none;
}
</style>
