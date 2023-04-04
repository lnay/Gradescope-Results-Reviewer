<script>
  import { query_selector_all } from "svelte/internal";

  export let data;

  // Filtering vars
  let pattern = ".*";
  $: test_filter = (test)=>test.number.match(pattern);
</script>

<style>
td {
  vertical-align: top;
}
.failed::before{
  content: "❌";
}
.passed::before{
  content: "✅";
}
.visible::before {
  content: "👁️";
}
</style>

{#if data}
<h1> Submission {data.num} </h1>
<h1> Name: {data.details[":submitters"][0][":name"]} </h1>

<input bind:value={pattern}/>
<br/>

<button on:click={
  ()=>{
    query_selector_all("td > details").forEach( (details)=>{
      details.open = true;
    });
  }
}>Open all outputs</button>

<button on:click={
  ()=>{
    query_selector_all("td > details").forEach( (details)=>{
      details.open = false;
    });
  }
}>Close all outputs</button>

<table>
<tbody>
{#each data.details[":results"].tests.filter(test_filter) as test}
  <tr>
    <td title="test number">{test.number}</td>
    <td title="test result: {test.status}" class={test.status}/>
    <td>
      {#if !(test.score===null)}
      {test.score}/{test.max_score}
      {/if}
    </td>
    <td title="test visibility: {test.visibility}" class={test.visibility}/>
    <td>
      {#if test.output}
       <details>
        <summary>{test.name}</summary>
        <pre>{test.output}</pre>
       </details>
      {:else}
       {test.name}
      {/if}
    </td>
  </tr>
{/each}
</tbody>
</table>
{/if}
