<script lang="ts">
  const emojis: {[key: string]: string} = {
    apple: "🍎",
    banana: "🍌",
    carrot: "🥕",
    doughnut: "🍩",
    egg: "🥚"
	};

	// the name is updated whenever the prop value changes...
	export let name: string;

	// ...but the "emoji" variable is fixed upon initialisation of the component
	// for it to be reactive you would need $:, but in this use case every dom element of the list would get updated, after removing an element
	const emoji = emojis[name];
</script>

<p>
	<span>The emoji for { name } is { emoji }</span>
</p>

<style>
	p {
		margin: 0.8em 0;
	}
	span {
		display: inline-block;
		padding: 0.2em 1em 0.3em;
		text-align: center;
		border-radius: 0.2em;
		background-color: #FFDFD3;
	}
</style>