<script lang="ts">
	import type { Mint } from '../../model/mint';
	import { token } from '../../stores/tokens';
	import { getAmountForTokenSet, getTokensForMint } from '../util/walletUtils';
	export let selectedMint: Mint;

	export let selectedDenomination = 1;
	export let selectedNumberOfNotes = 1;

	const availableAmount = getAmountForTokenSet(getTokensForMint(selectedMint, $token));

	const getDenominations = () => {
		const denos = Array<number>();
		let current = 1;
		while (current <= availableAmount) {
			denos.push(current);
			current = current * 2;
		}
		return denos;
	};

	const denomintations = getDenominations();
</script>

<div class="flex gap-2 flex-col ">
	<p>
		Selected Mint: {selectedMint.mintURL}
	</p>
	<p>
		Amount Available: {availableAmount} sats
	</p>
	<h2 class="font-bold text-lg text-center">Choose a denomination for the notes</h2>
	<div class="max-h-64 overflow-y-scroll">
		{#each denomintations as deno}
			<div class="max-w-xs lg:max-w-lg flex">
				<label class="label cursor-pointer">
					<input
						type="radio"
						name="radio-mint"
						class="radio checked:bg-primary"
						bind:group={selectedDenomination}
						value={deno}
					/>
					<span class="pl-2 label-text">{deno} sats</span>
				</label>
			</div>
		{/each}
	</div>
	<div class="flex gap-2 items-center">
		<p>number of notes:</p>
		<input type="number" class="input input-primary" bind:value={selectedNumberOfNotes} />
		(min. 1 - max. {Math.floor(availableAmount / selectedDenomination)})
	</div>
</div>
