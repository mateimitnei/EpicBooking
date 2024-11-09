<script>
	export let text = "Button";
	export let cancel = false;

	$: colorClass = cancel ? "bg-gray-500 hover:bg-gray-600 float-left" : "bg-sky-700 hover:bg-sky-600 float-right";
</script>

<button class={`text-lg mt-6 px-4 py-2 text-white rounded-xl transition ${colorClass}`} on:click>
	{text}
</button>
