<template>
  <div class="container">
    <GaTop/>
    <GaCon/>
  </div>
</template>

<script>
import GaTop from "@/components/GaTop";
import GaCon from "@/components/GaCon";

export default {
  name: 'App',
  components: {GaTop, GaCon},

}
</script>

<style>
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}
</style>
