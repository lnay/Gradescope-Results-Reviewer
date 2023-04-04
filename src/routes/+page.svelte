<script>
  import { onMount } from 'svelte';
  import DarkToggle from "../lib/DarkToggle.svelte";
  import SubmissionIndividual from "../lib/SubmissionIndividual.svelte";
  import PythonFileView from "../lib/PythonFileView.svelte";
  import yaml from "js-yaml";

  let focused_submission = null;
  let focused_file_path = null;
  let focused_file_component = PythonFileView;

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
      focused_file_path = null;
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
{#if focused_submission}

  <button on:click={
    ()=>{ focused_file_path = focused_submission.dir + "/task1.py";}
  }>task1.py</button>
  <button on:click={
    ()=>{ focused_file_path = focused_submission.dir + "/task2.py";}
  }>task2.py</button>
  <button on:click={
    ()=>{ focused_file_path = focused_submission.dir + "/task3.py";}
  }>task3.py</button>

  <SubmissionIndividual
    data={focused_submission}
    />
{/if}
</div>

<div class="right-pane">
  {#if focused_file_path}
  <svelte:component this={PythonFileView} path={focused_file_path}/>
  {/if}
</div>
