<script>
	import '$lib/app.css';

	let value = false;

	const promise = () => new Promise((resolve) => setTimeout(resolve, 2000));

	const generateArray = () =>
		Array(5)
			.fill(null)
			.map((i, ii) => ii);
</script>

<main class="flex h-screen flex-col place-content-center items-center gap-5">
	{#await promise()}
		<h1 class="text-2xl text-blue-600 animate-pulse font-bold">Loading...</h1>
	{:then}
		<h1 class="text-blue-400 text-2xl font-bold">Loaded</h1>
	{/await}

	{#await promise() then}
		<h1 class="font-bold text-blue-400 text-2xl">Loaded without status</h1>
	{/await}

	{#if value}
		<h1 class="text-2xl font-bold text-blue-400">Value is {value}</h1>
	{:else}
		<button
			class="rounded-md bg-blue-500 px-6 py-2 font-bold text-white hover:bg-blue-400"
			on:click={() => (value = true)}>Click to display value</button
		>
	{/if}
	<ul class="list-inside list-disc">
		{#each generateArray() as item}
			<li class="py-2 font-bold">Item # {item + 1}</li>
		{/each}
	</ul>
</main>
