<script lang="ts">
  //Components can also define their own event and fire them
  import { createEventDispatcher } from "svelte";
  
  //The createEventDispatcher needs to get called when the components get initalized
  //Calling it with setTimeout callback is not possible
  //For typing: each valid event key is a property, that gets assigned the type of the payload
  const dispatch = createEventDispatcher<{message: {text: string}}>();

  function sayHello() {
    dispatch('message', {
      text: 'Hello!'
    });
  }
</script>

<button on:click={sayHello}>
  Click to say hello
</button>