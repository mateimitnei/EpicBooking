<script>
	export let showModal = false;
</script>

{#if showModal}
	<div class="fixed inset-0 bg-black bg-opacity-40">
		<div class="bg-white p-10 pb-16 rounded-lg max-w-md mx-auto mt-20 text-center shadow-lg">
			<slot></slot>
		</div>
	</div>
{/if}
