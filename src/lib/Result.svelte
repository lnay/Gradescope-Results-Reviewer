<script>
  import { query_selector_all } from "svelte/internal";

  export let tests;
  export let test_filter = function(_test){return true;};
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

<button on:click={
  ()=>{
    query_selector_all("td > details").forEach( (details)=>{
      details.open=true;
    });
  }
}>Open all outputs</button>

<button on:click={
  ()=>{
    query_selector_all("td > details").forEach( (details)=>{
      details.removeAttribute("open");
    });
  }
}>Close all outputs</button>

<table>
<tbody>
{#each tests.filter(test_filter) as test}
  <tr>
    <td title="test result: {test.status}" class={test.status}/>
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
