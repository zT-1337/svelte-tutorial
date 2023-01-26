<script lang="ts">
  import Outer from "./Outer.svelte";
  import CustomButton from "./CustomButton.svelte";

  let m = {x: 0, y: 0};

  function handleMousemove(event: MouseEvent) {
    m.x = event.clientX;
    m.y = event.clientY;
  }

  function handleClick() {
    alert("Only this once");
  }

  function handleMessage(event: CustomEvent<{text: string}>) {
    console.log("hello");
    alert(event.detail.text);
  }

  function handleCustomButtonClick() {
    alert("Handled via bubbling");
  }
</script>

<!--Events are prefixed with on:-->
<!--All the html events are available-->
<div on:mousemove={handleMousemove}>
  The mouse position is {m.x} x {m.y}
</div>

<!--Event handles can also be defined inline like that-->
<!--Using inline or functions as event handlers has no impact on the performance-->
<div on:mousemove={e => m = {x: e.clientX, y: e.clientY}}>
  The mouse position is {m.x} x {m.y}
</div>

<!--Event handlers can have modifiers to change their behaviour-->
<!--The modifier is seperated with | from the event-->
<!--once modifier only allow the event handler to get called once-->
<!--Modifiers can be chained by using another |-->
<button on:click|once={handleClick}>
  Click me
</button>

<!--Custom events get handled the same way-->
<Outer on:message={handleMessage}/>

<CustomButton on:click={handleCustomButtonClick}/>

<style>
  div {
    width: 100%;
    height: 100%;
  }
</style>