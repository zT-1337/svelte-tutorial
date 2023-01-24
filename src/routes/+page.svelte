<script lang="ts">
  import Nested from "../components/Nested.svelte";

  let name = "Thomas"
  let src = "/favicon.png"
  let alt = "Svelte favicon"
  let htmlMarkup = `this string contains some <strong>HTML!!!</strong>`;
</script>

<h1>Welcome, {name}</h1>
<img {src} {alt}>
<p>This is a paragraph</p>
<Nested />
<!-- Be cautious of XSS attacks if the content of htmlMarkup is not trustworthy -->
<p>{@html htmlMarkup}</p>


<style>
  p {
    color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
  }
</style>
