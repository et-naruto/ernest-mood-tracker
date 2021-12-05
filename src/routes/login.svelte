<div class="card mt-5 m-auto text-center" style="width: 24em;">
    <div class="card-body">
   	 <h5 class="card-title">Welcome</h5>
   	 <p class="card-text text-muted">Please log-in to continue...</p>
   	 <form class="form-floating" on:submit|preventDefault={loginUser}>
   		 <input class="form-control" type="email" bind:value={email}/>
   		 <label for="floatingInput">Email address</label>
   		 <button type="submit" class="btn btn-dark mt-3">Magic</button>
   	 </form>
    </div>
</div>

<script>
    import supabase from '$lib/db';
    let email;
	async function loginUser() {
   	 const { error } = await supabase.auth.signIn({
   		 email
   	 });

   	 if (error) alert(error.message); // alert if error
	}
</script>