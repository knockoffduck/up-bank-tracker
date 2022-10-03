<script>
	import papa from 'papaparse';
	import Dropzone from 'svelte-file-dropzone';
	import '../app.scss';
	import Table from './table.svelte';
	let parsed = [];
	let headers;
	let files = {
		accepted: [],
		rejected: []
	};

	function csvParse(csvFile) {
		papa.parse(csvFile, {
			header: true,
			skipEmptyLines: true,
			complete: (results) => {
				parsed = results.data;
			}
		});
	}

	function handleFilesSelect(e) {
		const { acceptedFiles, fileRejections } = e.detail;
		files.accepted = [...files.accepted, ...acceptedFiles];
		files.rejected = [...files.rejected, ...fileRejections];
		csvParse(files.accepted[0]);
	}
	$: if (parsed.length > 0) {
		headers = parsed[0];
		console.log(Object.keys(headers));
	}
</script>

<section class="section">
	<div class="container">
		<h1 class="title has-text-centered">UP Bank Transactions Tracker</h1>
		<h3 class="has-text-centered">Upload CSV</h3>
	</div>
</section>

<div class="container">
	<Dropzone on:drop={handleFilesSelect} />
	<ul>
		{#await parsed}
			<p>loading...</p>
		{:then parsed}
			<div class="container">
				<Table tableData={parsed} />
			</div>
		{/await}
	</ul>
</div>
