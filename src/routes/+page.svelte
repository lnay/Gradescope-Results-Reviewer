<script>
  import { onMount } from 'svelte';
  import DarkToggle from "../lib/DarkToggle.svelte";
  import SubmissionIndividual from "../lib/SubmissionIndividual.svelte";
  import PythonFileView from "../lib/PythonFileView.svelte";
  import yaml from "js-yaml";

  let focused_submission = null;

  let submissions_data = null;
  onMount(async () => {
		const res = await fetch(`submissions/submission_metadata.yml`);
		let submissions_yaml = await res.text();
    submissions_data = yaml.load(submissions_yaml);
	});
</script>

<style>
div.left-pane {
  left: 0;
  width: 33%;
  position: absolute;
}
div.mid-pane {
  left: 33%;
  width: 33%;
  position: absolute;
  border-left: 2px solid currentColor;
  padding-left: 2px;
}
div.right-pane {
  right: 0;
  width: 33%;
  position: absolute;
  border-left: 2px solid currentColor;
  padding-left: 2px;
}
</style>

<DarkToggle/>
<br/>

<div class="left-pane">
{#if submissions_data}
  <table>
  <tr>
  <th> number </th>
  <th> name </th>
  <th> score </th>
  </tr>
  {#each Object.entries(submissions_data) as [key, value]}
    <tr on:click={()=>{
      focused_submission = {
        num: key.substring(11),
        dir: key,
        details: value
      };
    }}
    >
      <td>{key.substring(11)}</td>
      <td>{value[":submitters"][0][":name"]}</td>
      <td>{value[":results"].score}</td>
    </tr>
  {/each}
  </table>
{/if}
</div>

<div class="mid-pane">
<SubmissionIndividual
  data={focused_submission}
  />
</div>

<div class="right-pane">
<svelte:component this={PythonFileView} path="submission_165851132/task1.py"/>
</div>
