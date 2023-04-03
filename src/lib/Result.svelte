<script>
	export let tests;
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
{#each tests as test}
	<tr>
		<td class={test.status}>{test.status}</td>
		<td>{test.name}</td>
	</tr>
{/each}
</tbody>
</table>
