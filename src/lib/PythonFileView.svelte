<script>
import Highlight from "svelte-highlight";
import atomOneDark from "svelte-highlight/styles/atom-one-dark";
import python from "svelte-highlight/languages/python";
import { beforeUpdate, onMount } from 'svelte';
export let path="aoeu";

let file_content = null;
beforeUpdate(async () => {
  const res = await fetch("submissions/"+path);
  file_content = await res.text();
});
</script>

<svelte:head>
  {@html atomOneDark}
</svelte:head>

<p>
Path: {path}
</p>

{#if file_content}
  <Highlight language={python}  code={file_content} />
{/if}

