<script>
  import { onMount } from 'svelte';
  import DarkToggle from "../lib/DarkToggle.svelte";
  import yaml from "js-yaml";

  let submissions_data = null;

  onMount(async () => {
		const res = await fetch(`submissions/submission_metadata.yml`);
		let submissions_yaml = await res.text();
    submissions_data = yaml.load(submissions_yaml);
	});
</script>

<DarkToggle/>
<br/>

{#if submissions_data}
  <table>
  <tr>
  <th> submission number </th>
  <th> name </th>
  <th> score </th>
  </tr>
  {#each Object.entries(submissions_data) as [key, value]}
    <tr>
      <td>{key.substring(11)}</td>
      <td>{value[":submitters"][0][":name"]}</td>
      <td>{value[":results"].score}</td>
    </tr>
  {/each}
  </table>
{/if}
