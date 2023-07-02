<script lang="ts">
    import Time from "svelte-time";
    export let params: any = {};
    let user_data: any;
    let userId: number = params.id

    async function fetchData() {
		const response = await fetch(`https://admin.dev.orcam.io/api/v8/users/${userId}`, {
                    headers: {
                        Authorization: "accessKey d5797433-f9e0-4c83-aba4-58cd1e3bab4a"
                    }
                    })
		user_data =  await response.json();
	};

		fetchData();
</script>

<style>
.about-text p {
  font-size: 18px;
  max-width: 450px;
}

.about-list {
  padding-top: 10px;
}

.about-list .media {
  padding: 5px 0;
  font-size: 17px;
}

.about-list label {
  color: #20247b;
  font-weight: 600;
  width: 105px;
  margin: 0;
  position: relative;
}

.about-list label:after {
  content: "";
  position: absolute;
  top: 0;
  bottom: 0;
  right: 8px;
  width: 1px;
  height: 12px;
  background: #20247b;
  -moz-transform: rotate(15deg);
  -o-transform: rotate(15deg);
  -ms-transform: rotate(15deg);
  -webkit-transform: rotate(15deg);
  transform: rotate(15deg);
  margin: auto;
  opacity: 0.5;
}

.about-list p {
  margin: 0;
  width: 78%;
  word-wrap: break-word
}

.about-avatar {
    margin-top: 60px;
}

img {
    max-width: 100%;
    vertical-align: middle;
    border-style: none;
}

@media (max-width: 767px) {
  .about-text h3 {
    font-size: 35px;
  }
   .about-list p {
    width: 60%;
    }
}
</style>


{#if user_data === undefined}
    <section class="section about-section gray-bg" id="about">
        <div class="container">
            <div class="about-text go-to">
                <h3 class="dark-color">Loading User's Details...</h3>
            </div>
        </div>
    </section>
{:else}
    <section class="section about-section gray-bg" id="about">
        <div class="container">
            <div class="row align-items-center flex-row-reverse">
                <div class="col-lg-6 col-md-12 col-sm-12 col-xs-12">
                    <div class="about-text go-to">
                        {#if user_data.firstName === null  || user_data.lastName === null}
                            <h3 class="dark-color">Missing Name</h3>
                        {:else}
                            <h3 class="dark-color">{user_data.firstName} {user_data.lastName}</h3>
                        {/if}
                        <div class="row about-list">
                            <div class="col">
                                <div class="media">
                                    <label>Created At</label>
                                    <p><Time timestamp={user_data.createdAt} format="dddd · MMMM D, YYYY · h:mm A " /></p>
                                </div>
                                {#if user_data.updatedAt !== null}
                                    <div class="media">
                                        <label>Updated At</label>
                                        <p><Time timestamp={user_data.updatedAt} format="dddd · MMMM D, YYYY · h:mm A " /></p>
                                    </div>
                                {/if} 
                                {#if user_data.role !== null}
                                    <div class="media">
                                        <label>Role</label>
                                        <p>{user_data.role}</p>
                                    </div>
                                {/if}
                                {#if user_data.phone !== ""}
                                <div class="media">
                                    <label>Phone</label>
                                    <p>{user_data.phone}</p>
                                </div>
                                {/if}
                                <div class="media">
                                    <label>E-mail</label>
                                    <p>{user_data.email}</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-lg-6 col-md-12 col-sm-12 col-xs-12">
                    <div class="about-avatar">
                        <img src="https://bootdey.com/img/Content/avatar/avatar7.png" title="" alt="">
                    </div>
                </div>
            </div>
        </div>
    </section>
{/if}

