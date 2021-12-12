<script>
	import EntryModal from '$lib/EntryModal.svelte';
	import Greetings from '$lib/Greeting.svelte';
	import Entry from '$lib/Entry.svelte';
	import supabase from '$lib/db';
	async function signOut() {
		const { error } = await supabase.auth.signOut();

		if (error) alert(error.message); // alert if error
	}
	async function getEntries() {
		const { data, error } = await supabase.from('moodEntries').select();
		if (error) alert(error.message);

		return data;
	}
</script>

<div>
	<EntryModal />
</div>
<Greetings />
<!-- Entries -->
<section class="container px-4 py-3">
	<div class="d-flex justify-content-between">
		<div class="p-2">Mood Log</div>
		<input
			class="btn btn-light mb-2"
			type="button"
			value="+ New Entry"
			data-bs-toggle="modal"
			data-bs-target="#newEntry"
		/>
	</div>

	<div class="list-group mb-3">
		<!-- Individual Entries -->
		{#await getEntries()}
			<div class="loader">
				<span></span>
				<span></span>
				<span></span>
			</div>
		{:then data}
			{#each data as entry}
				<Entry
					date={entry.day + '-' + entry.month + '-' + entry.year}
					mood={entry.mood}
					comment={entry.comment}
				/>
			{/each}
		{:catch error}
			<p>Something went wrong while fetching the data:</p>
			<pre>{error}</pre>
		{/await}
	</div>
</section>

<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
	<button class="btn btn-secondary" on:click={signOut}>Logout</button>
</section>

<style>
	.loader {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.loader > span {
		display: inline-block;
		background-color: purple;
		width: 16px;
		height: 16px;
		border-radius: 50%;
		margin: 0 8px;
		animation: bounce 0.6s infinite alternate;
	}

	.loader > span:nth-child(2) {
		background-color: palevioletred;
	}

	@keyframes bounce {
		to {
			width: 16px;
			height: 16px;
			transform: translate3d(0, -16px, 0);
		}
	}
</style>

