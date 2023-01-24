<script lang="ts">
  export let name: string;
  export let version: string;
  export let speed: string;
  export let website: string;
</script>

<!--Props can also be accessed via $$props, even those that are not defined-->
<p>The version {version} of <code>{name}</code> is blazingly {speed}. Download at <a href={website}>{$$props.website}</a></p>