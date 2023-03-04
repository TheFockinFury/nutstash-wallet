<script lang="ts">
    import { getAmountForTokenSet, getTokensForMint } from '../../comp/util/walletUtils';
	import { mints } from '../../stores/mints';
	import { token } from '../../stores/tokens';
    
	export let selectedMint = $mints[0];
    
</script>
<p class="text-center font-bold text-lg">
    select a mint to print money from
</p>
{#each $mints.filter((m) => m.isAdded) as mint}
	<div class="max-w-xs lg:max-w-lg flex">
		<label class="label cursor-pointer">
			<input
				type="radio"
				name="radio-mint"
				class="radio checked:bg-primary"
				bind:group={selectedMint}
				value={mint}
			/>
			<span class="pl-2 label-text">{mint.mintURL}</span>
		</label>
	</div>
{/each}
<div class="border-dashed border-spacing-2 border-base-100 border-2">
	Available Tokens: {getAmountForTokenSet(getTokensForMint(selectedMint, $token))} sats
</div>
