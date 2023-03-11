<script lang="ts">
	import { CashuMint, CashuWallet, getEncodedProofs } from '@cashu/cashu-ts';
	import type { Mint } from '../../model/mint';
	import { pendingTokens } from '../../stores/pendingtokens';
	import { token } from '../../stores/tokens';
	import LoadingCenter from '../LoadingCenter.svelte';
	import { getTokensForMint, getTokensToSend, getTokenSubset } from '../util/walletUtils';
	import Note from './Note.svelte';

	export let selectedMint: Mint;
	export let selectedDenomination: number;
	export let selectedNumberOfNotes: number;

	let isFinished = false;
	let isLoading = false;

	const tokens = Array<string>();

	const printMoney = () => {
		handlePrint();
	};

	const handlePrint = (counter = 0) => {
		isLoading = true;
		counter++;
		const cashuMint = new CashuMint(selectedMint.mintURL);
		const cashuWallet = new CashuWallet(selectedMint.keysets, cashuMint);

		console.log(cashuMint.mintUrl)
		
		
		const tokensForMint = getTokensForMint(selectedMint, $token);
		const tokensToSend = getTokensToSend(selectedDenomination, tokensForMint);
		cashuWallet
			.send(selectedDenomination, tokensToSend)
			.then(({ returnChange, send }) => {
				//remove all tokens that have been sent to mint from storage
				token.update((state) => getTokenSubset(state, tokensToSend));
				//add the tokens that are being sent to pending
				pendingTokens.update((state) => [...send, ...state]);
				//add newly minted tokens that have been returned as change
				token.update((state) => [...state, ...returnChange]);

				tokens.push(
					getEncodedProofs(send, [{ url: selectedMint.mintURL, ids: selectedMint.keysets }])
				);
				if (counter < selectedNumberOfNotes) {
					setTimeout(() => {
						handlePrint(counter);
					}, 1000);
				} else {
					isFinished = true;
					isLoading = false;
				}
			})
			.catch((e) => {
				console.error(e);
				isLoading = false;
			});
	};
</script>

<svelte:head>
	<link rel="stylesheet" href="/tutorial/dark-theme.css" />
</svelte:head>

{#if isFinished}
	<div>
		{#each tokens as token}
			<p>
				{token}
			</p>
		{/each}
	</div>
{:else if isLoading}
	<LoadingCenter />
{:else}
	<div class="">
		<h2 class="font-bold text-lg text-center">Notes are ready to be printed</h2>
		<div class="flex flex-col gap-1">
			<p>
				Number of notes: {selectedNumberOfNotes}
			</p>
			<p>
				Denomination: {selectedDenomination}
			</p>
			<p>
				total value: {selectedDenomination * selectedNumberOfNotes}
			</p>
			<p class="max-w-xs overflow-clip truncate">
				From mint: {selectedMint.mintURL}
			</p>
		</div>
		<p class="font-bold">Preview:</p>
		<Note
			denomination={selectedDenomination}
			mintUrl={selectedMint.mintURL}
			token={'blablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablablabla'}
		/>
		<button class="btn btn-primary mt-2" on:click={printMoney}> BRRRRRR </button>
	</div>
{/if}

<style>
	@font-face {
		font-family: 'testfont';
		src: url('/fonts/super-car.otf');
	}
</style>
