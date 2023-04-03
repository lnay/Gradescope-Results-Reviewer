<script>
	export let tests;
	export let test_filter = function(_test){return true;};
</script>

<style>
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
		<td class={test.status}></td>
		<td class={test.visibility}></td>
		<td>{test.name}</td>
	</tr>
{/each}
</tbody>
</table>
