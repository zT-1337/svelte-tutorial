<script lang="ts">
  import Inner from "./Inner.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher<{message: {text: string}}>();

  //DOM Events bubble up until they find an event handler
  //Component/CustomEvents dont do that
  //Therefore you need to forward them yourself
  function forward(event: CustomEvent<{text: string}>) {
    dispatch('message', event.detail);
  }
</script>

<!--Forwarding the event-->
<Inner on:message={forward} />

<!--But this takes a lot of effort, so you can use that syntax for automatic event forwarding-->
<Inner on:message />