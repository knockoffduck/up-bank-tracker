<script>
	import Dropzone from 'svelte-file-dropzone';
	let result;

	function handleFilesSelect(e) {
		const { acceptedFiles, fileRejections } = e.detail;
		files.accepted = [...files.accepted, ...acceptedFiles];
		files.rejected = [...files.rejected, ...fileRejections];
		parseXML(file.accepted[0]);
	}
	function parseXML(file) {
		result = parser.toJson(file);
		console.log(result);
	}
</script>

<div class="container">
	<Dropzone on:drop={handleFilesSelect} />
</div>
