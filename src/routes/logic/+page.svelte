<script lang="ts">
  import Thing from "./Thing.svelte";
  import Await from "./Await.svelte";

  const user = {loggedIn: false};
  let x = 7;

  function toggle() {
    user.loggedIn = !user.loggedIn;
  }

  let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];

	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' },
	];

	function handleClick() {
		things = things.slice(1);
	}
</script>

<!--# indicates a block opener-->
<!--: indicates a block continuation-->
<!--/ indicates a block ending-->
{#if user.loggedIn}
 <button on:click={toggle}>Log out</button>
{:else}
  <button on:click={toggle}>Log in</button>
{/if}

{#if x > 10}
<p>x is bigger than 10</p>
{:else if x > 5}
<p>x is bigger than 5</p>
{:else}
<p>x is smaller than 5</p>
{/if}

<!--You can also get the current index, but dont have to-->
<!--The destructuring of cat is also possible {id, name}-->
<ul>
  {#each cats as cat, i}
    <li>
      <a target="_blank" href="https://www.youtube.com/watch?v={cat.id}" rel="noreferrer">
        {i + 1}: {cat.name}
      </a>
    </li>
  {/each}
</ul>

<button on:click={handleClick}>Remove Thing</button>

<!--(thing.id) defines a key that should be used for each element-->
<!--if there is no key provided, svelte always removes the last element and updates the reactive data of the remaining dom elements-->
<!--updates like that would be expensive, because every dom element needs to change, instead of just removing one-->
<!--The emoji variable of Thing could be made reactive, but then every element would get updated by removing one element-->
<!--With this approach only the first element gets removed and the others are untouched-->
{#each things as thing (thing.id)}
  <Thing name={thing.name}/>
{/each}

<Await />