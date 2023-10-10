<script lang="ts">
    let files: FileList;
    $: {
        if (files) {
            const chunkSize = 1024 * 1024; // 1MB
            const reader = new FileReader();
            const file = files[0];
            reader.onload = () => {
                const result: string = reader.result as string;
                console.log(result)
                const chunks = [];
                for (let i = 0; i < result.length; i += chunkSize) {
                    chunks.push(result.slice(i, i + chunkSize));
                }
                console.log(chunks)
            };
            reader.readAsBinaryString(file);
        }
    }
</script>

<input type="file" bind:files={files} />
