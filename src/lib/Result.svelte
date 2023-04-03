<script>
	export let tests;
	export let test_filter = function(_test){return true;};
</script>

<style>
.passed {
	background-color: green;
	color: white;
}
.failed {
	background-color: red;
	color: white;
}
</style>

<table>
<tbody>
{#each tests.filter(test_filter) as test}
	<tr>
		<td class={test.status}>{test.status}</td>
		<td>{test.name}</td>
	</tr>
{/each}
</tbody>
</table>
