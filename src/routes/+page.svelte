<script lang="ts">
  import { onMount } from 'svelte';
  import DarkToggle from "../lib/DarkToggle.svelte";
  import SubmissionIndividual from "../lib/SubmissionIndividual.svelte";
  import PythonFileView from "../lib/PythonFileView.svelte";
  import JupyterNotebookView from "../lib/JupyterNotebookView.svelte";
  import yaml from "js-yaml";

  let focused_submission = "";
  let focused_file_path = "";
  let focused_file_component = PythonFileView;

  let jupyter_server_url = "http://localhost:8888/";
  let jupyter_server_token = "";

  const SUBMISSION_FILES = [
    {
      name: "task1.py",
      viewer_component: PythonFileView,
    },
    {
      name: "task2.py",
      viewer_component: PythonFileView,
    },
    {
      name: "task3.py",
      viewer_component: PythonFileView,
    },
    {
      name: "A1.ipynb",
      viewer_component: JupyterNotebookView,
    },
  ]

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
  width: 20%;
  position: absolute;
  height: 100%;
  overflow:scroll;
}
.focused {
  background-color: red;
}
div.mid-pane {
  left: 20%;
  width: 39%;
  position: absolute;
  border-left: 2px solid currentColor;
  padding-left: 2px;
  height: 100%;
  overflow:scroll;
}
div.right-pane {
  right: 0;
  width: 39%;
  position: absolute;
  border-left: 2px solid currentColor;
  padding-left: 2px;
  height: 100%;
  overflow:scroll;
}
</style>

<div class="left-pane">
<DarkToggle/>
<br/>

<label>
  Jupyter server url:
  <input bind:value={jupyter_server_url}/>
</label>
<br/>
<label>
  Jupyter server token:
  <input bind:value={jupyter_server_token}/>
</label>

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
      focused_file_path = "";
    }}
      class={(focused_submission&&focused_submission.dir===key)?"focused":""}
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

  {#each SUBMISSION_FILES as file}
    <button on:click={
      ()=>{
        focused_file_component = file.viewer_component;
        focused_file_path = focused_submission.dir + "/" + file.name;
      }
    }>{file.name}</button>
  {/each}

  <SubmissionIndividual
    data={focused_submission}
    />
{/if}
</div>

<div class="right-pane">
  {#if focused_file_path}
  <svelte:component
    this={focused_file_component}
    path={focused_file_path}
    {jupyter_server_url}
    {jupyter_server_token}
    />
  {/if}
</div>
