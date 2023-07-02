<script lang="ts">
	import Router from "svelte-spa-router";
	import UsersList from "./components/users-list.svelte";
	import UserDetail from "./components/user-detail.svelte";
	import About from "./components/about.svelte";

	let routes: {[key: string]: any} = {
		"/" : UsersList,
		"/users/:id" : UserDetail,
		"/about" : About
	}
</script>

	
<main>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css"> 
	<Router {routes} />
</main>
