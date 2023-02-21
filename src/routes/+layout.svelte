<script>
  import "../app.css";
  import Navbar from "../lib/navbar.svelte";
</script>

<main class="bg-[#665b49] min-h-screen h-full min-w-full pb-40">
    <Navbar />
    <slot />
</main>
