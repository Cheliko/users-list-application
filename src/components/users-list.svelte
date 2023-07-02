<script lang="ts">
    import {onMount} from "svelte";
    import InfiniteScroll from "../InfiniteScroll.svelte";
    import UserItem from "./user-item.svelte";

	
    let page:number = 0;
	// store all the data here.
	let users: any[] = [];
	// store the new batch of data here.
	let newBatch: any[] = [];
	
	async function fetchData() {
		const response = await fetch("https://admin.dev.orcam.io/api/v8/users?page=0&size=10&sort=email:desc", {
		headers: {
			Authorization: "accessKey d5797433-f9e0-4c83-aba4-58cd1e3bab4a"
		}
		});
		let data: any = await response.json();
		newBatch = data.items;
	};
	
	onMount(()=> {
		// load first batch onMount
		fetchData();
	})

  $: users = [
	...users,
    ...newBatch
  ];
</script>

<style>
    
    .list-bg {
        margin-top: 3%;
    }
        
    .block {
        background: #fff;
        border-width: 0;
        border-radius: .25rem;
        box-shadow: 0 1px 3px rgba(0, 0, 0, .05);
        margin-bottom: 1.5rem
    }


    .list {
        padding-left: 0;
        padding-right: 0;
        max-height: 70vh;
        overflow-y: scroll;
    }

    .list::-webkit-scrollbar {
        width: 0.5em;
    }

    .list::-webkit-scrollbar-track {
        background-color: rgb(245, 245, 245);  
    }

    .list::-webkit-scrollbar-thumb {
        background-color: rgb(212, 209, 209);
    }


</style>

<main>
    <section class="section gray-bg list-bg">
        <div class="align-items-center flex-row-revers">
            {#if users[0] === undefined}
                <div class="about-text go-to">
                    <h3 class="dark-color">Loading List of Users...</h3>
                </div>
            {:else}
                <h3 class="dark-color">Users:</h3>
                <div class="padding">
                        <div class="list list-row block">
                                {#each users as user}
                                    <UserItem {user} />
                                {/each}
                                <InfiniteScroll
                                    hasMore={newBatch.length}
                                    threshold={100}
                                    on:loadMore={() => {page++; fetchData()}} />
                        </div>
                </div>
            {/if}
        </div>
    </section>
</main>