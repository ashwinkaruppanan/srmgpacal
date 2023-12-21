<script>
  import "../app.css";
  import Footer from "../lib/Footer.svelte";

  $: load = false;

  setTimeout(() => {
    load = true;
  }, 0);
</script>

{#if load}
  <slot />
  <Footer />
{/if}
