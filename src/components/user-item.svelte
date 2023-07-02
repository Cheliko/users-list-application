<script lang="ts">
    import {pop, push, replace} from "svelte-spa-router"
    export let user: any = {}
</script>

<style>
.item-detail {
	font-weight: 700;
}

.item-detail:hover {
    text-decoration: underline;
}

.w-48 {
    width: 48px!important;
    height: 48px!important;
	font-size: 24px;
}

  .circle {
    color: #fff;
    border: none;
    background: #31c971 linear-gradient(45deg, #31c971, #3dc931)
}
</style>

<div class="list-item" data-id="{user.userId}" on:click={() => { push(`/users/${user.userId}`)}}>
    <div><span class="w-48 avatar circle">👨🏻‍🦰</span></div>
    <div class="flex">
    {#if user.firstName === null  || user.lastName === null}
        <a href="/#/users/{user.userId}" class="item-author text-color" data-abc="true">Missing Name</a>
    {:else}
       <a href="/#/users/{user.userId}" class="item-author text-color" data-abc="true">{user.firstName} {user.lastName}</a>
    {/if}
       <div class="item-except dark-color text-sm h-1x">{user.email}</div>
    </div>
    <div class="no-wrap">
       <div class="item-detail dark-color text-sm">View Details</div>
    </div>
</div>

