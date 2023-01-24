<script lang="ts">
  import Child from './Child.svelte';
  import AnotherChild from './AnotherChild.svelte';

  const pkg = {
    name: 'svelte',
    speed: 'fast',
    version: '3',
    website: 'https://svelte.dev/'
  }
</script>

<Child />
<Child answer={"42"}/>

<AnotherChild {...pkg}/>