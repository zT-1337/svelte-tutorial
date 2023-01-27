<script lang="ts">
  let name = "world";

  let a = 1;
  let b = 2;

  let checked = false;

  let sizes = [
    "One Scoop",
    "Two Scoops",
    "Three Scoops"
  ];
  let scoops = 1;

  let menu = [
    "Cookies and Cream",
    "Mint choc chip",
    "Raspberry ripple"
  ];
  let flavours = [menu[1]];

  function join(flavours: string[]) {
    if(flavours.length === 1) return flavours[0];

    return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
  }

  let questions = [
    {id: 1, text: "first question"},
    {id: 2, text: "second question"},
    {id: 3, text: "third question"},
  ];

  let selected: {id: number; text: string};
  let answer = "";

  function handleSubmit() {
    alert(`answered question ${selected.id} '${selected.text}' with answer '${answer}'`)
  }

  let html = "<p>Write some text!</p>";

  let width = 0;
  let height = 0;
</script>

<!--bind directive activates the two way data binding-->
<!--otherwise it is only a one way binding-->
<!--change of name is set in the input, but change in the input does not affect name-->
<input bind:value={name}/>

<button on:click={() => name = "other"}>click me</button>
<h1>Hello {name}</h1>

<!--In the DOM everything is a string, so before using the value of input you need to convert it to a number first-->
<!--bind: does this for you-->
<label class="flex">
  <input type=number bind:value={a} min=0 max=10/>
  <input type=range bind:value={a} min=0 max=10/>
</label>

<label class="flex">
  <input type=number bind:value={b} min=0 max=10/>
  <input type=range bind:value={b} min=0 max=10/>
</label>

<p>{a} + {b} = {a + b}</p>

<label>
  <input type=checkbox bind:checked={checked}/>
  Yes! send me spam mail
</label>

{#if checked}
  <p>Thanks for consenting with spam</p>
{:else}
  <p>You have to consent</p>
{/if}

<button disabled={!checked}>Subscribe</button>

<h2>Size</h2>
<!--You can also bind inside of each blocks-->
{#each sizes as size, index}
  <label>
    <input type=radio bind:group={scoops} name="scoops" value={index + 1}/>
    {size}
  </label>
{/each}

<h2>Flavours</h2>
{#each menu as flavour}  
  <label>
    <input type=checkbox bind:group={flavours} name="flavours" value={flavour}/>
    {flavour}
  </label>
{/each}
<!--Instead of checkboxes you can also use select multiple-->
<select multiple bind:value={flavours}>
  {#each menu as flavour}
    <option value={flavour}>
      {flavour}
    </option>
  {/each}
</select>

{#if flavours.length === 0}
  <p>Please select atleast one flavour</p>
{:else if flavours.length > scoops}
  <p>You cant select more flavours than scoops</p>
{:else}
  <p>You ordered {scoops} {scoops === 1 ? "scoop" : "scoops"} of {join(flavours)}</p>
{/if}

<h2>Insecurity questions</h2>
<form on:submit|preventDefault={handleSubmit}>
  <!--Because selected has not initial value, the first option gets set as value-->
  <!--But until the binding is initialized the value of selected remains undefined, so be careful-->
  <select bind:value={selected} on:change={() => answer = ""}>
    {#each questions as question}
      <option value={question}>
        {question.text}
      </option>
    {/each}
  </select>
  <input bind:value={answer}/>
</form>

<p>selected question {selected ? selected.id : '[waiting...]'}</p>

<div contenteditable="true" bind:innerHTML={html}/>
<pre>{html}</pre>

<style>
  .flex {
    display: flex;
  }
  input, p {
    margin: 6px;
  }
</style>