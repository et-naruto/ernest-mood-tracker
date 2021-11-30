<script>
    import EntryModal from "$lib/EntryModal.svelte"
    import Greetings from "$lib/Greeting.svelte"
    import Entry from "$lib/Entry.svelte"
</script>
<EntryModal/>
<Greetings/>
<!-- Entries -->
<section class="container px-4 py-3">
    <div class="d-flex justify-content-between">
   	 <div class="p-2">Mood Log</div>
   	 <input class="btn btn-light mb-2" type="button" value="+ New Entry"data-bs-toggle="modal"
        data-bs-target="#newEntry"/>
    </div>

    <div class="list-group mb-3">
   	 <!-- Individual Entries -->
    	<Entry />
   	 
    </div>
</section>
