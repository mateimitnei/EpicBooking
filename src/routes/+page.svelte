<script>
	import Modal from './Modal.svelte';
	import Button from './Button.svelte';
	import DateButton from './DateButton.svelte';

	let showModal = false;
	let numOfPeople = ''; // Default to a valid number
	let name = ''

	let toggleModal = () => {
		showModal = !showModal;
	};
	let erase = () => {
		toggleModal();
		numOfPeople = '';
		name = '';
	};
	let handleInput = ({ target }) => {
		const value = target.value;
		if (value[0] === '-' || value === '0') {
			numOfPeople = 1; // Reset to 1 if value is less than 1
		}
	};
</script>

<Modal {showModal} on:click={toggleModal}>
	<p class="text-xl mb-3">Make a reservation</p>
	<form>
		<input type="text" bind:value={name} placeholder='Name' class="mb-4 rounded-lg w-full">
		<input type="number" bind:value={numOfPeople} placeholder='Number of people' class="mb-8 rounded-lg w-full" on:input={handleInput}>
	</form>
	<Button text="Cancel" cancel={true} on:click={erase}></Button>
	<Button text="Next" cancel={false} on:click={toggleModal}></Button>
</Modal>

<main>
	<div class="flex justify-center mt-60 bg-sky-700 w-fit m-auto rounded-3xl px-3">
		<DateButton text="02/01/2025" cancel={false} on:click={toggleModal}></DateButton>
		<DateButton text="03/01/2025" cancel={false} on:click={toggleModal}></DateButton>
		<DateButton text="18/02/2025" cancel={false} on:click={toggleModal}></DateButton>
		<DateButton text="19/02/2025" cancel={false} on:click={toggleModal}></DateButton>
	</div>
</main>
