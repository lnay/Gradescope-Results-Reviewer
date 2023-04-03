<script>
	export let resultData;
</script>

<style lang="css">
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
{#each resultData.tests as test}
	<tr>
		<td class={test.status}>{test.status}</td>
		<td>{test.name}</td>
	</tr>
{/each}
</tbody>
</table>
