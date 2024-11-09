<script>
	export let date = "unknown";
	export let price = null;
</script>

<button class="m-5 px-5 pb-3 pt-5 border-2 border-t-8 border-sky-600 text-sky-100 bg-sky-700 hover:bg-sky-600 rounded-2xl transition" on:click>
	{date}
	<br><br>
	<strong>{price} RON</strong>
</button>
