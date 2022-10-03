<script>
	export let tableData;
	let headers = ['Merchant', 'Amount', 'Type'];
</script>

<table class="table mx-auto">
	<thead>
		<tr>
			{#each headers as header}
				<th>
					{header}
				</th>
			{/each}
		</tr>
	</thead>
	<tbody>
		{#each tableData as { Merchant, Amount, Type }}
			<tr>
				<td>{Merchant}</td>
				<td>{Amount}</td>
				<td>{Type}</td>
			</tr>
		{/each}
	</tbody>
</table>
