<script lang="ts">
  import { query_selector_all } from "svelte/internal";

  export let data: any;

  // Filtering vars
  let pattern = ".*";

  type Test = {
    name: string,
    number: string,
    status: string,
    visibility: string,
    output: string,
  };

  $: test_filter = (test: Test)=>test.number.match(pattern);

  const AVAILABLE_PATTERNS:
  {
    label: string,
    pattern: string,
  }[] = [
    {
      label: "All",
      pattern: ".*"
    },
    {
      label: "1",
      pattern: "^1"
    },
    {
      label: "2",
      pattern: "^2"
    },
  ];
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

<h3> Refine: </h3>
<input bind:value={pattern}/>
<br/>

<h4> Predefined Refines: </h4>
{#each AVAILABLE_PATTERNS as elem}
<button on:click={()=>{
  pattern = elem.pattern;
}}>{elem.label}</button>
{/each}
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
