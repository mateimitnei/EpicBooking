<script>
	import Modal from './Modal.svelte';
	import Button from './Button.svelte';
	import DateButton from './DateButton.svelte';
	// Datele pentru rezervari din fisierul json:
	import days from '../data.json';

	let showModal = false,
		numOfPeople = '',
		name = '',
		stage = 1,
		error = '',
		selectedDate = '',
		selectedPrice = 0;

	let toggleModal = () => {
		showModal = !showModal;
		stage = 1;
	};
	let openModal = (date = '', price = 0) => {
		selectedDate = date;
		selectedPrice = price;
		toggleModal();
	};
	let nextModal = () => {
		if (name === '' || numOfPeople === '') {
			error = 'Ups... Completează tot!';
			return;
		}
		stage = 2;
		error = '';
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
	<div slot="content">
		{#if stage === 1}
			<p class="text-xl mb-4">Fă o rezervare</p>
			<form>
				<input type="text" bind:value={name} placeholder='Numele tău întreg' class="mb-4 rounded-xl w-full">
				<input type="number" bind:value={numOfPeople} placeholder='Numărul de locuri' class="mb-4 rounded-xl w-full"
							 on:input={handleInput}>
			</form>
			<p class="text-red-500">{error}</p>
		{:else if stage === 2}
			<p class="text-xl mb-7">Rezervare pentru <strong>{name}</strong> de <strong>{numOfPeople}</strong>
				{#if numOfPeople === 1}loc{:else}locuri{/if}:</p>
			<p class="text-xl mb-3 bg-sky-50 text-sky-800 rounded-xl p-2">Data: {selectedDate}</p>
			<p class="font-bold text-xl mb-3 bg-sky-50 text-sky-800 rounded-xl p-2">Preț total: {numOfPeople * selectedPrice}
				RON</p>
		{:else}
			<div class="flex flex-col items-center">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 text-green-500 mb-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
				</svg>
				<p class="text-xl mb-7">Rezervarea a fost procesată cu succes!</p>
			</div>
		{/if}
	</div>
	<div slot="buttons">
		{#if stage === 1}
			<Button text="Renunță" cancel={true} on:click={erase}></Button>
			<Button text="Mai departe" cancel={false} on:click={nextModal}></Button>
		{:else if stage === 2}
			<Button text="Renunță" cancel={true} on:click={erase}></Button>
			<Button text="Plătește" cancel={false} on:click={() => {stage = 3;}}></Button>
		{:else}
			<Button text="Închide" cancel={false} on:click={erase}></Button>
		{/if}
	</div>
</Modal>

<main>
	<h1 class="bg-sky-600 text-sky-200 text-4xl text-center p-7">Calendarul evenimentului</h1>
	<div
		class="grid grid-cols-2 w-96 justify-center mt-40 m-auto rounded-3xl p-3 border-8 border-sky-200 border-t-sky-600">
		{#each days as day}
			<DateButton date={day.date} price={day.price} cancel={false}
									on:click={() => openModal(day.date, day.price)}></DateButton>
		{/each}
	</div>
</main>
