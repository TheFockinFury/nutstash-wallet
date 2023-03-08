<script lang="ts">
	import Step1 from '../../comp/brrr/Step1.svelte';
	import Step2 from '../../comp/brrr/Step2.svelte';
	import Step3 from '../../comp/brrr/Step3.svelte';
	import type { Mint } from '../../model/mint';

	let step = 1;

	let selectedMint: Mint;
	let selectedDenomination: number;
	let selectedNumberOfNotes: number;

	const nextStep = () => {
		if (step > 2) {
			return;
		}
		step++;
	};
	const previousStep = () => {
		if (step < 2) {
			return;
		}
		step--;
	};
</script>

<div class="flex m-2 gap-2 flex-col">
	<div>
		<a href="/" class="btn"> back </a>
	</div>

	<h1 class="text-center font-bold text-2xl">Money printer go brrrrr</h1>
	<ul class="steps">
		<li data-content="🏦" class="step step-primary" />
		<li data-content="💵" class="step {step > 1 ? 'step-primary' : ''}" />
		<li data-content="🖨️" class="step {step > 2 ? 'step-primary' : ''}" />
	</ul>
	<div class="m-auto">
		{#if step === 1}
			<Step1 bind:selectedMint />
		{:else if step === 2}
			<Step2 bind:selectedMint bind:selectedDenomination bind:selectedNumberOfNotes />
		{:else}
			<Step3 bind:selectedMint bind:selectedDenomination bind:selectedNumberOfNotes />
		{/if}
	</div>
	<div class="flex justify-center w-full gap-2">
		<button class="btn {step === 1 ? 'btn-disabled' : ''}" on:click={previousStep}> back </button>
		{#if step <= 2}
			<button class="btn btn-primary" on:click={nextStep}> continue </button>
		{/if}
	</div>
</div>
