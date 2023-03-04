<script lang="ts">
	import { QRCodeImage } from 'svelte-qrcode-image';
	import type { Mint } from '../../model/mint';

	export let selectedMint: Mint;
	export let selectedDenomination: number;
	export let selectedNumberOfNotes: number;
</script>

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
	</div>
	<p class="font-bold">Preview:</p>

	<div class="w-96 h-72 bg-black rounded-2xl flex content-center items-center">
		<div class="bg-white w-80 h-36 m-auto p-0.5 ">
			<div class="border w-full h-full border-solid p-1 flex flex-col items-center justify-between">
				<div class="overflow-clip w-full text-xxs">
					<code>
						Issued by:
					</code>
                    <code>
						{selectedMint.mintURL}
					</code>
				</div>
                <div class="flex w-full h-full items-center justify-between">
				<div class="flex flex-col justify-between h-full">
					<div
						class="border border-gray-500 border-solid rounded-full w-10 h-10 flex items-center justify-center text-xs"
					>
						<code>
							{selectedDenomination}
						</code>
					</div>

					<div
						class="border border-gray-500 border-solid rounded-full w-10 h-10 flex items-center justify-center text-xs"
					>
						<svg
							class="w-4 h-4"
							stroke="currentColor"
							fill="currentColor"
							id="Layer_1"
							data-name="Layer 1"
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 360 360"
							><rect x="166.06" y="2.83" width="27.89" height="47.65" /><rect
								x="166.06"
								y="310.35"
								width="27.89"
								height="47.65"
							/><rect
								x="166.06"
								y="6.84"
								width="27.89"
								height="198.86"
								transform="translate(286.28 -73.74) rotate(90)"
							/><rect
								x="166.06"
								y="80.5"
								width="27.89"
								height="198.86"
								transform="translate(359.94 -0.08) rotate(90)"
							/><rect
								x="166.06"
								y="152.08"
								width="27.89"
								height="198.86"
								transform="translate(431.52 71.5) rotate(90)"
							/></svg
						>
					</div>
				</div>

				<div class="flex items-center justify-center">
					<QRCodeImage text="asdf" scale={4.1} displayType="canvas" />
				</div>
				<div class="flex flex-col justify-between h-full">
					<div
						class="border border-gray-500 border-solid rounded-full w-10 h-10 flex items-center justify-center text-xs"
					>
						<svg
							class="w-4 h-4"
							stroke="currentColor"
							fill="currentColor"
							id="Layer_1"
							data-name="Layer 1"
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 360 360"
							><rect x="166.06" y="2.83" width="27.89" height="47.65" /><rect
								x="166.06"
								y="310.35"
								width="27.89"
								height="47.65"
							/><rect
								x="166.06"
								y="6.84"
								width="27.89"
								height="198.86"
								transform="translate(286.28 -73.74) rotate(90)"
							/><rect
								x="166.06"
								y="80.5"
								width="27.89"
								height="198.86"
								transform="translate(359.94 -0.08) rotate(90)"
							/><rect
								x="166.06"
								y="152.08"
								width="27.89"
								height="198.86"
								transform="translate(431.52 71.5) rotate(90)"
							/></svg
						>
					</div>
					<div
						class="border border-gray-500 border-solid rounded-full w-10 h-10 flex items-center justify-center text-xs"
					>
						<code>
							{selectedDenomination}
						</code>
					</div>
				</div>
                
			</div>
            <div class="overflow-clip w-full text-xxs">
                <code>
                    {selectedMint.mintURL}
                </code>
            </div>    
		</div>
        
	</div>
</div>

	<div>
		<div>
			selectedMint: {selectedMint.mintURL}
		</div>
		<div>
			selectedDenomination: {selectedDenomination}
		</div>
	</div>
	<button class="btn btn-primary"> BRRRRRR </button>
</div>
