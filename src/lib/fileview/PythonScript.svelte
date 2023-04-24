<script lang="ts">
import Highlight from "svelte-highlight";
import atomOneDark from "svelte-highlight/styles/atom-one-dark";
import python from "svelte-highlight/languages/python";
import { beforeUpdate } from 'svelte';

export let path: string;

let file_content: string | null = null;

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

