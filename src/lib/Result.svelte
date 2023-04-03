<script>
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

<table>
<tbody>
{#each tests.filter(test_filter) as test}
  <tr>
    <td title="test result: {test.status}" class={test.status}></td>
    <td title="test visibility: {test.visibility}" class={test.visibility}></td>
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
