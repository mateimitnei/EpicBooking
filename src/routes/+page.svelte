<script>
	import Modal from './Modal.svelte';
	import Button from './Button.svelte';
	import DateButton from './DateButton.svelte';
	import days from '../data.json';

	let showModal = false;
	let numOfPeople = '';
	let name = '';
	let stage = 1;
	let error = '';
	let selectedDate = '';
	let selectedPrice = 0;

	let toggleModal = () => {
		showModal = !showModal;
		stage = 1;
	};
	let nextModal = () => {
		if (name === '' || numOfPeople === '') {
			error = 'Ups... Completează tot!';
			return;
		}
		stage = 2;
		error = '';
	};
	let openModal = (date = '', price = 0) => {
		selectedDate = date;
		selectedPrice = price;
		erase();
	};
	let erase = () => {
		toggleModal();
		numOfPeople = '';
		name = '';
		error = '';
	};
	let handleInput = ({ target }) => {
		const value = target.value;
		if (value[0] === '-' || value === '0') {
			numOfPeople = 1; // Reset to 1 if value is less than 1
		}
	};
</script>

<Modal {showModal} on:click={toggleModal}>
	{#if stage === 1}
		<p class="text-xl mb-4">Fă o rezervare</p>
		<form>
			<input type="text" bind:value={name} placeholder='Numele tău întreg' class="mb-4 rounded-xl w-full">
			<input type="number" bind:value={numOfPeople} placeholder='Numărul de locuri' class="mb-4 rounded-xl w-full"
						 on:input={handleInput}>
		</form>
		{#if error}
		{/if}
		<p class="text-red-500">{error}</p>
		<Button text="Renunță" cancel={true} on:click={erase}></Button>
		<Button text="Mai departe" cancel={false} on:click={nextModal}></Button>
	{/if}
	{#if stage === 2}
		<p class="text-xl mb-7">Reservation by {name} for {numOfPeople} people:</p>
		<p class="text-xl mb-3 bg-sky-50 text-sky-800 rounded-xl p-2">Date: {selectedDate}</p>
		<p class="font-bold text-xl mb-3 bg-sky-50 text-sky-800 rounded-xl p-2">Total price: {numOfPeople * selectedPrice} RON</p>
		<Button text="Renunță" cancel={true} on:click={erase}></Button>
		<Button text="Plătește" cancel={false} on:click={toggleModal}></Button>
	{/if}
</Modal>

<main>
	<h1 class="bg-sky-600 text-sky-200 text-4xl text-center p-5">Calendarul evenimentului</h1>
	<div class="grid grid-cols-2 w-96 justify-center mt-40 m-auto rounded-3xl p-3 border-8 border-sky-200 border-t-sky-600">
		{#each days as day}
			<DateButton date={day.date} price={day.price} cancel={false} on:click={() => openModal(day.date, day.price)}></DateButton>
		{/each}
	</div>
</main>
