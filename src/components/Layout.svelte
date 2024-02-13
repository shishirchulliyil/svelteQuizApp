<script>
  import Navigate from "./Navigate.svelte";
  import Footer from "./Footer.svelte";
</script>

<div>
  <!-- navigation component -->
  <Navigate />
  <!-- components -->
  <slot />
  <!-- footer component -->
  <Footer />
</div>
