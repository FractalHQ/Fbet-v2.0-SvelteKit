<script>
	import SectionIdentifier from '$lib/global/section_identifier.svelte';
	import TourneyCard from '$lib/tournaments/tourney_card.svelte';
	import { api_base_url, stored_token } from '$lib/global.js';
	import { onMount } from 'svelte';

	let tourneys = [];

	let get_tourneys_by_user_status = function () {
		fetch(api_base_url + '/tournament/get_tourneys_by_user_status', {
			method: 'GET',
			mode: 'cors',
			headers: {
				Authorization: 'Bearer ' + stored_token,
				Accept: 'application/json'
			}
		})
			.then((response) => response.json())
			.then((data) => {
				tourneys = data;
			})
			.catch((error) => {
				console.log(error);
				return [];
			});
	};

	onMount(async () => {
		get_tourneys_by_user_status();
	});
</script>

<SectionIdentifier section_name="Campeonatos" />

<section class="container-fluid">
	<div class="row">
		<div class="col-sm-10 mx-auto">
			{#each tourneys as tourney}
				<TourneyCard tourney_info={tourney} />
			{/each}
			<div class="row" id="tournaments-container" />
		</div>
	</div>
</section>
