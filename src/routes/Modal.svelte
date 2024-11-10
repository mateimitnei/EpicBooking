<script>
	export let showModal = false;
</script>

{#if showModal}
	<div class="fixed inset-0 bg-black bg-opacity-40">
		<div class="bg-white p-14 pb-32 rounded-2xl max-w-md mx-auto mt-48 text-center shadow-lg">
			<slot name="content"></slot>
			<slot name="buttons"></slot>
		</div>
	</div>
{/if}
