<script lang="ts">
	import { goto } from '$app/navigation';
	import { posisiBase } from '$lib/stores/posisiAndmin';

	export let total: number[];
	export let ketetapanBg: number[];
	const d = [''];

	let bg = [
		'text-slate-200 stroke-black stroke-2 ',
		'text-red-400',
		'text-violet-300',
		'text-orange-400',
		'text-pink-400',
		'text-lime-700 ',
		'text-fuchsia-600'
	];
	let bg2: string[] = [];
	// ketetapanBg = [0, 1, 2, 3, 4, 5, 6, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0];

	for (let i in ketetapanBg) {
		bg2.push(bg[ketetapanBg[i]]);
	}

	let currentKec = {
		nama: '',
		id: 0,
		x: 0,
		y: 0
	};
	let kecamatan = [
		{ nama: 'wadaslintang', id: 1, x: 260, y: 390 },
		{ nama: 'kepil', id: 2, x: 535, y: 390 },
		{ nama: 'sapuran', id: 3, x: 530, y: 320 },
		{ nama: 'kaliwiro', id: 4, x: 280, y: 340 },
		{ nama: 'leksono', id: 5, x: 330, y: 270 },
		{ nama: 'sukoharjo', id: 6, x: 270, y: 255 },
		{ nama: 'selomerto', id: 7, x: 330, y: 340 },
		{ nama: 'kalikajar', id: 8, x: 530, y: 270 },
		{ nama: 'kertek', id: 9, x: 510, y: 240 },
		{ nama: 'wonosobo', id: 10, x: 340, y: 300 },
		{ nama: 'watumalang', id: 11, x: 280, y: 220 },
		{ nama: 'mojotengah', id: 12, x: 330, y: 210 },
		{ nama: 'garung', id: 13, x: 490, y: 200 },
		{ nama: 'kejajar', id: 14, x: 450, y: 150 },
		{ nama: 'kalibawang', id: 15, x: 370, y: 360 }
	];
	if ($posisiBase == 1) {
		kecamatan = [
			{ nama: 'wadaslintang', id: 1, x: 460, y: 390 },
			{ nama: 'kepil', id: 2, x: 735, y: 390 },
			{ nama: 'sapuran', id: 3, x: 730, y: 320 },
			{ nama: 'kaliwiro', id: 4, x: 480, y: 340 },
			{ nama: 'leksono', id: 5, x: 530, y: 270 },
			{ nama: 'selomerto', id: 6, x: 530, y: 340 },
			{ nama: 'kalikajar', id: 7, x: 730, y: 270 },
			{ nama: 'kertek', id: 8, x: 710, y: 240 },
			{ nama: 'wonosobo', id: 9, x: 540, y: 300 },
			{ nama: 'watumalang', id: 10, x: 480, y: 220 },
			{ nama: 'mojotengah', id: 11, x: 530, y: 210 },
			{ nama: 'garung', id: 12, x: 690, y: 200 },
			{ nama: 'kejajar', id: 13, x: 650, y: 150 },
			{ nama: 'sukoharjo', id: 14, x: 470, y: 255 },
			{ nama: 'kalibawang', id: 15, x: 570, y: 360 }
		];
	} else {
		kecamatan = [
			{ nama: 'wadaslintang', id: 1, x: 260, y: 390 },
			{ nama: 'kepil', id: 2, x: 535, y: 390 },
			{ nama: 'sapuran', id: 3, x: 530, y: 320 },
			{ nama: 'kaliwiro', id: 4, x: 280, y: 340 },
			{ nama: 'leksono', id: 5, x: 330, y: 270 },
			{ nama: 'selomerto', id: 6, x: 330, y: 340 },
			{ nama: 'kalikajar', id: 7, x: 530, y: 270 },
			{ nama: 'kertek', id: 8, x: 510, y: 240 },
			{ nama: 'wonosobo', id: 9, x: 340, y: 300 },
			{ nama: 'watumalang', id: 10, x: 280, y: 220 },
			{ nama: 'mojotengah', id: 11, x: 330, y: 210 },
			{ nama: 'garung', id: 12, x: 490, y: 200 },
			{ nama: 'kejajar', id: 13, x: 450, y: 150 },
			{ nama: 'sukoharjo', id: 14, x: 270, y: 255 },
			{ nama: 'kalibawang', id: 15, x: 370, y: 360 }
		];
	}

	let masokk = false;
	const popFromText = (i: boolean, a: number) => {
		const b = kecamatan[a].nama;
		const divTotal = document.getElementById('ttoto')?.style;
		const target = document.getElementById(b)?.classList;
		if (i) {
			masokk = true;
			setTimeout(() => {
				divTotal!.display = 'flex';
			}, 100);

			if (ketetapanBg[a] !== 0) {
				target?.add('-translate-y-5', 'brightness-110', 'drop-shadow-xl');
			}
		} else {
			masokk = false;
			target?.remove('-translate-y-5', 'brightness-110', 'drop-shadow-xl');
			setTimeout(() => {
				if (!masokk) {
					divTotal!.display = 'none';
				}
			}, 900);
		}
	};
	let currentTotal = 0;
	const totalin = (x: number) => {
		currentTotal = total[x];
		currentKec = kecamatan[x];
		const divTotal = document.getElementById('ttoto')?.style;
		divTotal!.top = currentKec.y + 'px';
		divTotal!.left = currentKec.x + 'px';
	};
</script>

<!-- <div class="w-16 h-10 bg-slate-200 absolute"><h1>{totakPerKec}</h1></div> -->

<!-- Creator: CorelDRAW X7 -->
<div
	on:mouseleave={() => {
		popFromText(false, currentKec.id - 1);
	}}
	on:mouseenter={() => {
		popFromText(true, currentKec.id - 1);
		totalin(currentKec.id - 1);
	}}
	id="ttoto"
	style="top: 220px ; left:290px ; display:none;"
	class="absolute p-2 shadow-slate-900 shadow z-20 cursor-default transition-all duration-500 flex flex-col text-xs text-white justify-center bg-black bg-opacity-50 rounded-lg backdrop-blur"
>
	<h1>
		{currentKec.nama}
	</h1>
	<h1>
		total : {currentTotal}
	</h1>
</div>

<svg
	xmlns="http://www.w3.org/2000/svg"
	xml:space="preserve"
	width="3.01805in"
	height="3.65201in"
	version="1.1"
	style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd"
	viewBox="0 0 984 1214"
	xmlns:xlink="http://www.w3.org/1999/xlink"
>
	<defs>
		<filter id="whiteOutlineEffect" color-interpolation-filters="sRGB">
			<feMorphology in="SourceAlpha" result="MORPH" operator="dilate" radius="2" />
			<feColorMatrix
				in="MORPH"
				result="WHITENED"
				type="matrix"
				values="-1 0 0 0 1, 0 -1 0 0 1, 0 0 -1 0 1, 0 0 0 1 0"
			/>
			<feMerge>
				<feMergeNode in="WHITENED" />
				<feMergeNode in="SourceGraphic" />
			</feMerge>
		</filter>
	</defs>

	<g id="Layer_x0020_2">
		<metadata id="CorelCorpID_0Corel-Layer" />
		<g id="_2206784726448" font-size="30">
			<g
				on:mouseleave={() => {
					popFromText(false, 12);
				}}
				on:mouseenter={() => {
					popFromText(true, 12);
					totalin(12);
				}}
				on:click={() => {
					goto('nilai/13');
				}}
			>
				<path
					id="kejajar"
					class=" fill-current {bg2[12]} leading-tight transition-all duration-300"
					d="M542 0c-8,0 -8,6 -9,12 -2,7 -8,7 -12,12 -27,29 -6,35 -7,49 -1,6 -7,8 -11,13 -4,4 -7,11 -12,13 -4,1 -8,-1 -15,1 -12,3 -9,3 -22,3 -11,-1 -11,1 -20,4 -8,2 -27,0 -38,3 -7,1 -9,7 -15,10 -6,3 -12,4 -17,9 -4,5 -5,9 -10,14 -8,7 -8,5 -11,15 -4,21 -10,13 11,26 8,5 12,5 20,6 10,2 9,4 17,8 17,10 25,0 38,-6 17,-8 27,-3 44,-5 8,0 12,-3 22,-2 9,1 14,1 24,1 57,-4 37,-1 58,14 6,4 7,8 11,13 15,21 -4,27 21,23 13,-2 30,-5 41,4 13,9 19,6 33,17 17,14 28,34 53,48 3,2 14,9 17,9 5,-1 3,-15 1,-18 -3,-7 -5,-6 -5,-15 0,-5 0,-17 1,-22 6,-16 16,-19 5,-35 -4,-6 -3,-14 -7,-18 -4,-4 -10,-5 -16,-11 -27,-29 -28,-23 -42,-34 -6,-4 -7,-9 -12,-13 -7,-5 -9,-3 -15,-11 -6,-7 -7,-5 -14,-9 -12,-6 -21,-40 -31,-45 -6,-3 -11,-2 -17,-7 -6,-5 -7,-12 -10,-15 -3,-3 -6,3 -12,-2 -15,-13 -7,-21 -13,-33 -1,-1 -24,-26 -24,-26z"
				/>
				<text class="textOnMap" filter="url(#whiteOutlineEffect)" x="500" y="150" dx="-30"
					>Kejajar</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 9);
				}}
				on:mouseenter={() => {
					popFromText(true, 9);
					totalin(9);
				}}
				on:click={() => {
					goto('nilai/10');
				}}
			>
				<path
					id="watumalang"
					class=" fill-current {bg2[9]}  transition-all duration-300"
					d="M376 199c-12,-4 -12,0 -25,-8 -6,-3 -14,-10 -20,-8 0,2 1,1 0,6l-5 17c-3,7 -3,-2 -10,23 -2,7 -5,7 -8,12 6,11 4,5 -1,13 6,16 2,8 -3,19 -7,17 -7,6 -14,13 -3,2 -1,4 -3,8 -2,4 -8,12 -11,15 -4,4 -2,4 -5,8 -9,1 -5,0 -14,3 0,9 -1,6 -5,10 -7,8 -5,-1 -12,7 -11,12 -9,5 -14,23 -5,4 -16,6 -18,14 -2,12 -1,13 -14,19 -12,6 -14,-4 -22,6 -3,4 -3,6 -5,11 -2,5 -4,4 -7,8 3,8 22,15 23,15 9,1 14,-10 28,0 6,5 5,7 12,5 8,-3 8,-2 15,0 21,7 13,3 17,20 6,2 13,1 19,2 7,1 9,0 15,-4 8,-4 14,-14 27,-13 4,6 2,8 7,16 8,11 19,-1 23,19 1,5 5,6 10,10 4,2 6,1 10,2 7,1 3,2 7,4 5,3 10,0 18,4 15,7 18,-16 25,5 27,-14 15,-10 29,-7 10,-8 9,-13 11,-16 3,-5 3,1 3,-7 1,-8 3,-3 3,-9 -8,-1 -4,3 -19,-9 2,-4 2,-6 1,-10l-7 1c0,6 -1,10 -6,13 -8,5 -4,4 -9,10 -5,-2 -11,-8 -15,-12 -6,-6 1,-13 -11,-15 -1,9 3,2 -1,11 -2,5 -2,7 -2,12 0,0 -11,-8 -12,-8 -3,-3 -3,-9 -7,-13 -4,-4 -8,-8 -11,-10 -5,-4 -7,-5 -7,-13 -1,-48 -6,-28 9,-42 7,-5 9,-2 13,2 4,0 5,-2 8,-2 5,1 1,2 7,2 2,-6 3,-6 1,-12 7,-3 3,0 4,-3 0,0 1,-3 1,-4 3,-11 -2,-21 -2,-22 0,-4 2,-6 1,-10 -1,-3 -3,-4 -4,-9 -3,-16 -5,-23 4,-30 1,-10 -3,-5 5,-12 1,-11 -2,-7 3,-19 2,-4 2,-7 3,-11 1,-3 18,-34 16,-44 -8,1 -12,8 -27,4 -24,-5 -11,-7 -22,-10z"
				/>
				<text
					class=" -rotate-45 textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="-40"
					y="460"
					dx="-70">Watumalang</text
				>
			</g>

			<g
				on:mouseleave={() => {
					popFromText(false, 13);
				}}
				on:mouseenter={() => {
					popFromText(true, 13);
					totalin(13);
				}}
				on:click={() => {
					goto('nilai/14');
				}}
			>
				<path
					id="sukoharjo"
					class=" fill-current {bg2[13]}  transition-all duration-300"
					d="M301 594c-1,-4 -11,-5 -5,-21 19,-9 7,-8 15,-20 -6,-1 -10,0 -9,-8 1,-10 1,-6 6,-12 12,-14 2,-22 0,-28 -3,-12 11,-26 12,-26 3,-6 -1,-9 -3,-14 -1,-2 -6,-11 -7,-12 -10,1 -17,14 -26,16 -5,1 -33,-2 -36,-5 -5,-7 6,-15 -15,-19 -7,-2 -6,1 -11,2 -9,3 -13,-7 -19,-9 -6,-3 -14,5 -24,2l-19 -9c-4,2 -4,3 -7,5 -8,7 -6,-4 -12,22 -2,13 8,25 -3,34 -5,5 -2,-1 -5,7 -3,7 -13,13 -21,11 -9,-3 -9,-1 -11,8 -2,9 -7,6 -13,9 -6,26 -7,17 -9,23 -2,4 0,4 -3,9 -1,3 -4,2 -6,4 -3,3 -1,4 -4,7 -6,5 -7,-2 -15,0 4,2 6,0 10,5 13,15 10,4 23,8 7,2 3,4 7,8 4,5 2,0 9,8 3,5 6,3 10,5 11,5 10,9 15,17 16,1 5,-3 20,4 12,6 6,3 13,11 13,-5 13,1 26,1 6,0 5,-4 12,-1 4,2 5,5 8,7 14,1 16,4 27,6 5,-4 6,-11 9,-16 5,-10 -2,-10 3,-18 5,-1 5,1 10,1 6,1 3,-1 8,-3 8,-4 6,3 14,-8 5,-1 10,-1 15,-5 6,-5 7,-2 11,-6z"
				/>
				<text class="  textOnMap" filter="url(#whiteOutlineEffect)" x="190" y="540" dx="-70"
					>Sukoharjo</text
				>
			</g>

			<g
				on:mouseleave={() => {
					popFromText(false, 11);
				}}
				on:mouseenter={() => {
					popFromText(true, 11);
					totalin(11);
				}}
				on:click={() => {
					goto('nilai/12');
				}}
			>
				<path
					on:mouseenter={() => {}}
					id="garung"
					class=" fill-current {bg2[11]}  transition-all duration-300"
					d="M456 196c-2,6 2,1 5,19 1,9 2,13 3,23 0,3 1,21 1,23 2,5 9,11 9,17 0,12 -17,3 -2,35 4,8 0,12 6,18 8,6 6,11 14,13 11,-2 4,-10 17,-5 15,6 36,-9 43,5 7,15 0,12 0,20 8,1 23,-9 23,-9 24,-11 13,33 38,2 5,-5 17,-11 23,-12 5,0 10,1 16,1 18,-1 25,-4 39,-11 11,-5 46,-12 52,-16 0,-1 -27,-15 -32,-22 -5,-5 -10,-9 -15,-14 -6,-5 -8,-12 -13,-16 -6,-4 -10,-9 -17,-11 -11,-4 -10,-1 -20,-9 -11,-9 -33,-3 -47,0 -7,1 -16,8 -19,2 -5,-9 8,-10 6,-22 0,-1 -10,-18 -11,-19 -2,-2 -6,-3 -8,-5 -3,-3 -4,-6 -7,-8 -9,-6 -40,0 -52,-1 -10,0 -14,-2 -26,0 -8,2 -24,1 -26,2z"
				/>
				<text class="textOnMap " filter="url(#whiteOutlineEffect)" x="550" y="290" dx="-30"
					>Garung</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 10);
				}}
				on:mouseenter={() => {
					popFromText(true, 10);
					totalin(10);
				}}
				on:click={() => {
					goto('nilai/11');
				}}
			>
				<path
					id="mojotengah"
					class=" fill-current {bg2[10]}  transition-all duration-300"
					d="M440 198c-9,15 -12,31 -20,48 -11,23 -4,28 -16,50 -11,19 15,40 1,83 -3,10 -12,10 -21,11 -7,1 -15,-5 -18,1 -2,3 -2,23 -2,27 1,8 10,11 14,18 11,15 5,5 11,-2 7,-7 19,2 22,9 1,3 2,9 6,11 3,2 8,1 10,-3 3,-5 -7,-19 4,-17 5,1 7,2 13,2 3,-1 8,-4 10,-3 1,2 -2,31 6,18 5,-7 2,-21 2,-29 1,-15 12,-10 22,-15 7,-3 16,-11 25,-14 7,-4 3,15 7,23 2,4 12,20 17,19 8,0 11,-15 21,-4 29,32 27,22 43,13 9,-5 13,-12 22,-16 8,-5 16,-9 24,-13 6,-3 14,-13 21,-18 14,-11 35,-44 55,-58 3,-1 25,-11 11,-7 -9,3 -21,5 -30,8 -10,4 -17,9 -27,11 -28,7 -36,-5 -58,16 -5,5 -12,15 -19,11 -8,-5 -9,-19 -20,-13 -53,24 -26,-10 -31,-16 -5,-6 -21,1 -29,1 -4,0 -9,-1 -13,0 -5,0 -9,3 -14,4 -9,2 -11,-11 -18,-18 -7,-9 -4,-16 -9,-26 -5,-13 -8,-15 0,-28 6,-10 -5,-13 -6,-26 -1,-13 0,-22 -2,-36 -3,-12 -1,-21 -14,-22z"
				/>
				<text
					class="textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="520"
					y="190"
					dx="-0"
					transform="rotate(20 0,0)">Mojotengah</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 4);
				}}
				on:mouseenter={() => {
					popFromText(true, 4);
					totalin(4);
				}}
				on:click={() => {
					goto('nilai/5');
				}}
			>
				<path
					id="leksono"
					class=" fill-current {bg2[4]}  transition-all duration-300"
					d="M433 572c0,-4 -1,-8 0,-11 0,-6 0,-3 2,-7 1,-6 2,-12 2,-18 -2,-17 3,-27 2,-33 -5,-1 -14,4 -18,7 -11,10 -10,2 -15,-2 -18,2 -13,-1 -21,-4 -5,-2 -9,0 -14,-1 -4,-2 -3,-4 -8,-5 -6,-2 -5,0 -11,-4 -3,-2 -6,-3 -9,-5 -12,-7 -1,-13 -11,-17 -2,2 -11,21 -13,24 -3,8 -3,5 0,13 11,26 -15,27 -2,38 4,3 5,6 3,11 -5,9 -1,6 -3,13 -5,3 -6,2 -11,8 -5,7 0,5 3,9 7,9 -8,15 -12,20 -4,4 -6,2 -12,4 -8,2 -5,3 -11,7 -26,13 -13,6 -23,7 -1,4 0,5 -2,9 -1,3 -10,16 -11,20l8 9c7,0 11,-6 19,-3 2,0 13,9 14,10 1,7 -2,6 -2,13 0,19 -1,23 -13,32 0,3 1,9 1,13 1,4 -1,9 0,10 7,2 8,1 13,-3 7,-4 19,-1 31,-2 7,-1 7,-2 15,-2 11,0 20,-8 27,-4 6,3 19,10 23,10 2,-10 -18,-46 -12,-64 2,-6 2,-3 4,-5 4,-3 2,-2 4,-6 3,-7 6,-4 10,-9 2,-2 3,-4 5,-5 3,-3 3,-1 6,-3 7,-5 2,-4 12,-8 1,-8 -1,-2 3,-8l11 -25c5,-7 6,-8 8,-16 5,-22 6,-11 8,-17z"
				/>
				<text
					class=" textOnMap"
					filter="url(#whiteOutlineEffect)"
					transform="rotate(-60 0,0)"
					x="-340"
					y="620"
					dx="-70"
					>Leksono
				</text>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 8);
				}}
				on:mouseenter={() => {
					popFromText(true, 8);
					totalin(8);
				}}
				on:click={() => {
					goto('nilai/9');
				}}
			>
				<path
					id="wonosobo"
					class=" fill-current {bg2[8]}   transition-all duration-300"
					d="M523 590c13,-19 0,-26 6,-35 3,-6 18,-14 21,-22 7,-22 8,-12 20,-24 4,-4 6,-8 10,-11 5,-5 7,-4 12,-9l17 -15c3,-2 3,-4 6,-6 6,-4 5,-1 13,-8 2,-2 9,-5 13,-7 8,-6 4,-6 13,-9 8,-3 6,-6 11,-11 7,-10 2,-9 5,-17 1,-5 3,-3 3,-7 0,-1 -1,-5 -1,-8 -15,7 -5,13 -33,25 -4,2 -9,6 -12,7 -8,4 -6,1 -12,9 -3,3 -8,5 -12,8 -9,5 -14,14 -25,14 -5,-4 -11,-9 -17,-13 -6,-5 -8,-12 -15,-14 -4,3 -8,9 -14,9 -7,0 -25,-25 -27,-40 -13,6 -2,-1 -14,8 -9,7 -10,2 -18,4 1,6 0,6 -1,11 -3,8 -1,5 0,11 1,11 -7,9 -3,20 2,5 0,18 -3,21 -3,5 -3,6 -5,10 -3,3 -3,2 -6,7 -5,11 -11,4 -10,42 1,11 -15,40 6,39 7,-8 2,-13 13,-20 10,-5 14,-2 20,6 2,3 7,7 8,9 2,4 2,7 6,10 2,1 22,5 25,6z"
				/>
				<text
					class="textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="490"
					y="710"
					dx="-370"
					transform="rotate(-30 0,0) ">Wonosobo</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 7);
				}}
				on:mouseenter={() => {
					popFromText(true, 7);
					totalin(7);
				}}
				on:click={() => {
					goto('nilai/8');
				}}
			>
				<path
					id="kertek"
					class=" fill-current {bg2[7]}  transition-all duration-300"
					d="M683 411c-1,4 -4,4 -6,8 -1,4 0,8 -1,12 -3,12 -22,22 -26,26 -7,6 -9,5 -16,9 -3,2 -4,4 -7,6 -3,2 -6,2 -9,4 -7,5 -20,20 -28,25 -8,5 -6,6 -12,13 -6,6 -11,7 -15,11 -2,1 -7,15 -8,16 6,2 9,0 15,2 4,2 6,4 10,5 7,2 21,1 24,7 0,7 -10,10 -15,14 -3,3 -4,8 -4,12 -2,5 -1,4 3,8 15,13 15,28 23,37 6,-2 9,-6 13,-8 7,-4 10,3 17,-2 10,-6 6,0 14,-3 6,-2 8,-8 6,-13 -3,-8 -5,-8 0,-16 3,-5 3,-7 8,-12 12,-12 17,2 29,0 2,-4 0,-3 3,-7 7,-10 4,-10 19,-15 11,-3 6,-2 11,-10 2,-3 6,-6 10,-11 6,-1 13,-1 18,-6 2,-2 3,-5 5,-6 5,-4 4,-2 9,-4 5,-4 -1,-2 7,-4 2,0 5,-1 8,-3 9,-4 16,-21 23,-25 5,-3 15,2 26,-22 2,-6 7,-8 12,-11 -3,-9 -42,-50 -50,-56 -5,-4 -9,-9 -14,-13 -5,-4 -9,-9 -15,-12 -17,-12 -9,-20 -17,-35 -3,0 -29,14 -33,17 -6,4 -22,21 -26,26 -21,34 -10,29 -11,36z"
				/>
				<text
					class="textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="690"
					y="780"
					dx="-360"
					transform="rotate(-30 0,0) ">Kertek</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 6);
				}}
				on:mouseenter={() => {
					popFromText(true, 6);
					totalin(6);
				}}
				on:click={() => {
					goto('nilai/7');
				}}
			>
				<path
					id="kalikajar"
					class=" fill-current {bg2[6]}  transition-all duration-300"
					d="M962 545c-13,-4 -41,-23 -52,-38 -4,-6 -9,-6 -13,-11 -6,-5 -6,-12 -13,-17 -5,-4 -12,-7 -17,-12 -5,-4 -7,-10 -13,-11 -3,-1 -10,2 -12,5 -2,5 -1,9 -6,16 -3,4 -3,0 -7,4 -6,6 -3,8 -13,10 -6,1 -10,9 -13,14 -4,9 -25,14 -35,21 -8,5 -10,8 -19,11 -10,4 -8,4 -14,13 -4,6 -12,7 -18,10 -7,4 -8,9 -12,15 -10,16 -23,-9 -35,6 -11,16 6,20 -3,33 -12,16 -32,8 -44,14 -8,4 -6,11 -17,15 -7,3 -14,1 -18,7 -12,16 0,22 -24,36 -17,10 -14,15 -38,16 -9,0 -13,1 -19,9 -4,6 -13,9 -16,14 -3,6 6,12 8,20 2,8 0,10 11,9 6,-1 14,-1 19,-2 9,-3 8,-8 12,-11 9,-6 26,5 35,0 16,-9 17,-22 40,-8 10,6 15,3 25,0 7,-1 23,1 24,1 2,-1 3,-24 14,-29 9,-4 8,-2 16,-10 14,-16 43,-21 52,-27 15,-8 3,-18 32,-17 10,0 33,-1 40,6 6,6 4,11 4,18 0,0 9,-7 12,-9 16,-10 4,-25 25,-29 9,-2 7,1 15,-7 5,-5 10,-9 16,-13 7,-5 10,-9 18,-13 6,-3 14,-6 20,-10 7,-4 10,-8 18,-11 12,-5 6,-4 13,-11 3,-3 37,-16 2,-27z"
				/>

				<text
					class="textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="650"
					y="910"
					dx="-360"
					transform="rotate(-30 0,0) ">Kalikajar</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 2);
				}}
				on:mouseenter={() => {
					popFromText(true, 2);
					totalin(2);
				}}
				on:click={() => {
					goto('nilai/3');
				}}
			>
				<path
					id="sapuran"
					class=" fill-current {bg2[2]}  transition-all duration-300"
					d="M831 796c0,0 7,-15 8,-17 15,-30 27,-22 31,-41 2,-10 4,-8 9,-15 4,-5 6,-10 9,-15 6,-9 17,-18 21,-27 6,-10 15,-19 21,-29 4,-6 5,-9 9,-15 5,-5 9,-7 9,-13 0,-13 5,-25 14,-34 15,-16 22,-11 22,-19 -21,3 -19,8 -23,13 -3,3 -8,4 -13,6 -4,3 -7,6 -10,8 -9,6 -17,8 -25,13 -20,12 -13,12 -21,16 -11,5 -12,12 -23,16 -11,3 -17,2 -17,16 0,11 -11,11 -19,18 -5,5 -13,15 -21,15 -9,-8 3,-18 4,-26 -4,-5 -9,-8 -16,-7 -3,1 -6,3 -9,3 -5,0 -3,-2 -7,-2 -5,0 -2,3 -9,1 -4,-1 -4,-3 -8,-2 -8,3 -6,8 -11,13 -9,9 -38,13 -49,21 -4,3 -7,8 -12,12 -10,8 -17,11 -22,25 -6,20 -17,7 -35,12 -6,2 -13,4 -20,2 -13,-4 -13,-7 -16,-8 -6,-1 -11,5 -16,8 -3,2 -5,2 -8,4 -2,3 -1,3 -5,6 -4,-1 -4,-3 -9,-3 -6,-1 -4,0 -11,-2 -6,-2 -12,4 -14,9 2,5 5,5 9,7 -2,6 -4,11 1,15 4,4 6,8 9,10 10,1 8,-1 15,-5 4,-2 9,-4 13,-6 17,-8 16,3 23,10 5,4 10,4 14,7 20,16 9,38 11,44 0,0 19,15 7,25 -5,3 -24,13 -25,14 10,6 12,0 20,1 7,1 8,8 18,6 7,-2 8,-7 15,-10 12,-5 11,1 19,1 7,-5 11,-16 20,-14 6,4 8,40 22,41 13,2 12,4 15,4 -2,-5 -4,-3 -4,-11 1,-10 1,-5 0,-14 -2,-13 11,-10 18,-13 5,-9 4,-16 6,-25 9,-8 17,-2 27,-3 3,-3 13,-20 14,-24 1,-8 3,-7 8,-12 5,-5 4,-7 8,-12l9 2z"
				/>

				<text
					class="textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="550"
					y="1040"
					dx="-360"
					transform="rotate(-30 0,0) ">Sapuran</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 5);
				}}
				on:mouseenter={() => {
					popFromText(true, 5);
					totalin(5);
				}}
				on:click={() => {
					goto('nilai/6');
				}}
			>
				<path
					id="selomerto"
					class=" fill-current {bg2[5]}  transition-all duration-300"
					d="M606 635c1,-4 -8,-16 -10,-20 -5,-10 -4,-11 -12,-19 -9,-8 -14,-7 -8,-20 10,-21 10,-11 13,-18 -3,-3 -10,-1 -13,-3 -5,-1 -6,-4 -12,-5 -13,-1 -17,-2 -25,8 -7,8 3,19 -3,27 -7,11 -7,15 -21,11 -9,-2 -21,-2 -26,-9 -4,-6 -8,-17 -15,-21 -10,-5 -12,12 -15,17 -8,11 -19,0 -24,0 -2,3 -3,12 -6,17 -2,6 -6,9 -8,15 -2,7 -4,10 -7,17 -4,7 -1,12 -9,14 -10,5 -5,8 -13,10 -9,4 -19,15 -22,23 -3,7 1,13 2,19l11 37c4,10 29,2 39,3 6,1 13,3 20,4 16,4 35,29 43,24 3,-4 0,-7 4,-13 3,-5 4,-5 0,-11 -5,-8 -13,-14 -5,-25 3,-5 6,-3 10,-5 11,-6 11,-20 32,-18 12,1 40,-15 46,-25 5,-10 -2,-19 9,-25 4,-2 9,-5 11,-6 5,-2 9,0 14,-3z"
				/>
				<text class="textOnMap" filter="url(#whiteOutlineEffect)" x="470" y="680" dx="-70"
					>Selomerto</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 3);
				}}
				on:mouseenter={() => {
					popFromText(true, 3);
					totalin(3);
				}}
				on:click={() => {
					goto('nilai/4');
				}}
			>
				<path
					id="kaliwiro"
					class=" fill-current {bg2[3]}  transition-all duration-300 "
					d="M168 754c-20,-3 -26,5 -46,-3 -14,-5 -22,-1 -31,-5 -4,-2 -20,-12 -22,-14 -7,-6 -2,-4 -11,-6 -6,-1 -7,-1 -14,-1 -2,4 -5,12 -1,16 5,6 9,0 7,13l-11 34c6,6 9,5 11,14l9 2c1,4 0,6 0,9 1,3 1,4 2,8 2,15 2,7 4,14 1,4 -1,10 -1,15 -1,7 2,7 1,14 -4,4 -5,1 -8,6 -8,16 9,8 9,8 5,-1 6,0 12,-1 11,-4 8,-9 19,-2 4,3 4,1 10,2 7,0 4,1 10,-2 4,-2 7,-2 10,-5 3,-2 2,-4 7,-7 5,1 3,2 8,1 12,-3 9,3 17,14 11,16 -3,22 21,24 14,1 31,-1 45,2 7,1 13,1 20,-1 7,-2 4,-7 15,-7 5,4 1,4 9,6 4,2 5,2 9,4 9,5 1,3 6,7 3,3 0,-4 5,7 16,-15 4,-29 38,-20 7,11 9,6 18,8 4,1 12,10 17,10 1,-6 -1,-7 1,-12 5,-1 6,1 11,2 12,2 16,-8 34,1 5,3 41,-2 51,-2 0,-8 -3,-4 -1,-13 1,-5 -2,-5 -4,-9 1,-9 4,-8 7,-15 4,-10 -5,-25 -6,-33 -1,-7 -4,-11 -3,-17 9,-3 17,12 28,5 0,-6 -2,-6 -2,-14 4,-2 19,-11 23,-12 6,3 11,10 16,13 4,4 5,2 7,7 2,4 1,5 5,8 5,-9 7,-6 12,-15 2,-2 4,-6 5,-8 3,-4 15,-5 -1,-20 -8,-6 -4,-8 -6,-16 -2,-2 -3,-2 -5,-4 -8,-8 -2,-5 -15,-4 -6,1 -6,-1 -11,-1 -3,0 -5,2 -8,2 -3,0 -4,-2 -6,-2 -4,11 -4,18 -19,12 -23,-11 -3,-5 -21,-15 -6,-3 -4,-5 -12,-7 -26,-7 -29,-2 -48,-3 -8,0 -25,-2 -32,-5 -29,-15 -7,-4 -41,-3 -5,0 -9,2 -15,2 -6,0 -13,0 -18,0 -7,1 -7,3 -12,5 -7,2 -10,-1 -16,2 -18,7 -13,-1 -30,4 -7,3 -9,0 -16,-1 -15,-1 -19,7 -30,7 -7,1 -10,-2 -16,-3z"
				/>
				<text class="textOnMap" filter="url(#whiteOutlineEffect)" x="250" y="830" dx="-70"
					>Kaliwiro</text
				>
			</g>

			<g
				on:mouseleave={() => {
					popFromText(false, 0);
				}}
				on:mouseenter={() => {
					popFromText(true, 0);
					totalin(0);
				}}
				on:click={() => {
					goto('nilai/1');
				}}
			>
				<path
					id="wadaslintang"
					class="  fill-current {bg2[0]}  transition-all duration-300"
					d="M288 1101c6,-7 8,-20 11,-29 4,-11 18,0 30,-4 22,-9 5,-17 12,-24 3,-4 9,-2 10,-7 2,-4 -1,-9 2,-14 4,-7 20,-9 24,-15 -1,-5 -10,-8 -13,-15 -4,-8 -4,-16 5,-18 12,-4 41,-4 23,-23 -6,-7 -11,-3 -17,-12 -5,-8 -24,-24 -33,-25 -23,-4 -16,-7 -20,-9 -8,-1 -7,-2 -12,-3 -8,4 -6,8 -8,14 -2,4 -3,1 -6,5 -2,4 0,3 -4,7 -8,1 -5,-3 -9,-6 -5,-4 -6,2 -8,-7 -1,-6 -3,-5 -8,-7 -4,-2 -8,-5 -11,-6 -7,3 -3,5 -13,7 -14,2 -31,-2 -56,-2 -37,1 -25,-13 -33,-25 -2,-4 -5,-11 -7,-13 -3,0 -12,1 -14,3 -7,8 -5,4 -13,8 -12,5 -7,2 -17,2 -14,0 -4,0 -13,-5 -5,3 -6,7 -13,7 -5,1 -6,-3 -11,2 7,6 8,11 14,18 12,11 9,5 8,19 2,3 3,2 6,5 7,7 11,12 14,21 -9,4 -8,4 -18,3 -11,0 -23,14 -26,15 -5,1 -12,-2 -18,-2 -9,0 -7,4 -9,10 -1,5 -7,6 -12,8 -12,6 -23,1 -25,17 -1,7 2,11 2,18 0,7 -2,7 3,12 14,16 -2,17 2,31 5,15 2,24 2,39 0,9 4,7 11,10 4,2 7,7 11,10 8,9 9,9 16,26 4,9 4,22 12,30 3,4 8,6 12,9 8,7 9,3 17,4 9,2 5,5 17,4 7,0 10,0 16,3 7,4 7,9 10,11 3,2 6,-4 13,-2 7,1 6,5 16,6 5,0 16,2 19,2 7,-1 6,-8 11,-11 4,-4 8,0 10,-7 8,-24 10,-11 20,-21 -1,-6 -12,-14 6,-16 9,-2 8,12 17,8 1,-2 0,-13 1,-17 1,-11 1,-7 7,-13 5,-5 -10,-14 14,-20 23,-5 11,-2 23,-16z"
				/>
				<text class="textOnMap" filter="url(#whiteOutlineEffect)" x="150" y="1030" dx="-70"
					>Wadaslintang</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 1);
				}}
				on:mouseenter={() => {
					popFromText(true, 1);
					totalin(1);
				}}
				on:click={() => {
					goto('nilai/2');
				}}
			>
				<path
					id="kepil"
					class=" fill-current {bg2[1]}  transition-all duration-300"
					d="M682 884c1,5 4,12 -2,16 -6,3 -9,-1 -5,9 5,12 10,22 3,34 -5,7 0,4 3,9 2,6 -3,10 -1,17 6,16 23,13 20,23 -3,8 -7,3 -2,14 5,12 -15,44 -15,50 -1,5 2,7 0,15 -3,9 3,5 5,14 2,9 -3,8 6,9 10,2 10,4 13,12 3,12 17,12 26,8 10,-5 20,-10 28,0 5,7 -2,19 1,29 3,18 12,8 25,3 8,-3 7,-5 17,-5 7,0 9,1 6,-6 -6,-11 7,-28 4,-37 -1,-5 -7,-9 -4,-14 1,-1 11,-12 12,-13 6,-6 6,-4 13,-12 7,-8 9,-4 13,-7 3,-1 3,-5 9,-8 6,-4 3,-9 5,-15 3,-9 6,-7 1,-17 -2,-4 -4,-15 -7,-17 -3,-4 -9,-5 -8,-12 2,-7 16,-2 21,-2 6,0 9,-3 14,1 20,12 11,4 13,-10 0,-4 1,-16 2,-19 1,-3 3,-2 5,-10 2,-7 1,-14 2,-19 2,-5 8,-8 8,-13 0,-5 -8,-12 7,-31 11,-15 -3,-24 1,-39 4,-11 9,-25 18,-31 6,-4 1,-7 5,-13 3,-5 8,-6 10,-12 7,-16 -11,-10 -18,-23 -5,-10 -2,-28 -7,-41 -2,-4 -9,-12 -4,-16 4,-3 15,-2 17,-7 2,-4 -3,-6 -2,-11 0,-4 2,-13 3,-17 3,-18 10,-10 5,-32 -3,6 -2,-1 -4,5 -2,6 0,2 -4,4 2,11 -1,5 -5,11 -2,3 1,2 -2,6l-13 15c-6,9 -3,0 -6,12l-5 0c2,4 -7,15 -13,16 0,9 2,3 -3,10 -3,3 -4,7 -6,10 -3,3 -7,6 -8,9 -7,12 8,1 -17,27 -17,16 -4,3 -14,17 -10,12 -6,16 -8,19 -3,5 -7,5 -11,5 -6,1 -4,3 -8,7 -5,5 -4,2 -6,8 -3,8 -4,4 -5,9 -2,7 -2,4 -6,10 -4,5 -1,6 -5,10 -4,2 -16,2 -20,0 -4,-2 0,-2 -4,0 -3,1 -3,0 -5,1 1,4 3,6 3,11 -1,4 -2,3 -3,7 -3,16 -11,8 -21,14 0,4 2,3 2,9 -1,4 -3,5 -1,9 2,5 9,8 11,13 -5,1 -5,0 -11,2 -14,6 -7,-3 -18,-2 -15,2 -13,-3 -18,-10 -1,-2 -6,-22 -11,-29 -3,3 -20,20 -21,11z"
				/>

				<text
					class="textOnMap"
					filter="url(#whiteOutlineEffect)"
					x="550"
					y="1220"
					dx="-360"
					transform="rotate(-30 0,0) ">Kepil</text
				>
			</g>
			<g
				on:mouseleave={() => {
					popFromText(false, 14);
				}}
				on:mouseenter={() => {
					popFromText(true, 14);
					totalin(14);
				}}
				on:click={() => {
					goto('nilai/15');
				}}
			>
				<path
					id="kalibawang"
					class=" fill-current {bg2[14]}  transition-all duration-300"
					d="M532 835c-7,1 -9,-3 -12,-9 -4,-9 -4,-5 -10,-12 -4,-3 -8,-9 -13,-7 -1,1 -12,8 -13,9l5 9c-7,13 -23,5 -28,5 -2,10 3,14 5,20 7,19 -4,30 -5,32 -1,4 2,4 4,8 0,2 0,20 -1,22 -2,1 -47,5 -51,5 -14,-1 -4,-9 -33,-3 -6,1 -6,-1 -11,0 -2,9 1,8 12,21 5,6 15,7 20,14 10,13 2,19 5,26 3,6 9,14 16,15 4,-8 4,-14 14,-19 7,-2 4,-5 8,-8 1,-1 8,-6 9,-7 6,-4 4,2 11,-4 10,-8 21,4 37,5 5,-6 2,-6 11,-5 4,1 8,-1 13,-3 13,-4 13,3 24,9 4,3 22,-3 30,4 3,2 5,17 12,23 5,-1 6,-6 15,-5 8,1 4,4 15,0 2,-5 1,-15 8,-16 5,0 6,2 7,5 4,6 1,2 7,5 4,2 3,3 7,5 4,1 6,1 9,3 8,4 8,5 17,0 -1,-8 -6,-19 -6,-28 -1,-10 1,-19 4,-27 -7,-5 -5,-5 -8,-12 -2,-7 -5,-4 -5,-14 6,-5 6,-6 14,-7 -3,-6 -2,-6 -4,-10 -11,8 -16,15 -32,7 -9,-5 -8,0 -17,-1 -2,0 -15,-4 -16,-5 -3,-14 20,-18 30,-27 0,-13 -10,-6 -10,-20 0,-13 9,-28 -15,-39 -11,-5 -9,-10 -15,-14 -5,-2 -27,13 -29,13 -11,4 -17,11 -22,21 -4,8 -4,3 -8,7 -4,4 -1,5 -5,9z"
				/>
				<text class="textOnMap" filter="url(#whiteOutlineEffect)" x="550" y="920" dx="-70"
					>Kalibawang</text
				>
			</g>
		</g>
	</g>
</svg>
