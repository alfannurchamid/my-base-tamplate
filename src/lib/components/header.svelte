<script lang="ts">
	import { user, updateUser, lengkap } from "$lib/stores/userLogin";
	import Logo from "$lib/static/Logo.svg";

	import IconUser from "$lib/static/iconUser.svg";
	import { RefreshToken } from "$lib/stores/auth";
	import { onMount } from "svelte";
	import { GetCookie, logout, SetCookie } from "$lib/stores/cokies";
	// @ts-ignore

	let clickUser = false;

	const iconUserClick = () => {
		if ($lengkap) {
			clickUser = !clickUser;
			const target = document.getElementById("iconUser")?.classList;
			const seting = document.getElementById("pengaturan")?.classList;
			if (clickUser) {
				target?.remove("fill-black");
				target?.add("fill-red-400");
				seting?.remove(
					"translate-y-full",
					"backdrop-blur-none",
					"bg-opacity-0"
				);
				seting?.add(
					"backdrop-blur-xl",
					"bg-opacity-5",
					"backdrop-brightness-75"
				);
			} else {
				target?.remove("fill-red-400");
				target?.add("fill-black");
				seting?.remove(
					"backdrop-blur-xl",
					"bg-opacity-5",
					"backdrop-brightness-75"
				);
				seting?.add(
					"translate-y-full",
					"translate-y-full",
					"backdrop-blur-none",
					"bg-opacity-0"
				);
			}
		}
	};
	onMount(async () => {
		// console.log('start');
		let bahan = GetCookie("refreshkey");
		let accessKey = GetCookie("accesskey");
		console.log(bahan);
		if (!bahan) {
			logout();
		} else {
			accessKey = GetCookie("accesskey");
			if (!accessKey) {
				await RefreshToken(bahan);
			}
			let completeKey = GetCookie("complete");
			let complete = false;
			let deretKey = [
				1, 2, 3, 5, 1, 3, 2, 4, 5, 1, 1, 2, 3, 5, 1, 3, 2, 4, 5, 1, 1, 2, 3, 5,
				1, 3, 2, 4, 5, 1,
			];
			let tg1 = "";
			if (completeKey) {
				let bahan1 = String(bahan).slice(30, 60);
				if (bahan1) {
					for (let x = 0; x < completeKey?.length; x++) {
						let h = bahan1.charCodeAt(x);
						let i = String.fromCharCode(h + deretKey[x]);
						tg1 = tg1 + i;
					}
				}
				console.log(tg1);
				complete = true;
			}

			accessKey = GetCookie("accesskey");

			// console.log(accessKey);

			const response = await fetch(
				"http://127.0.0.1:8000/api/api/v1/auth/profile",
				{
					headers: {
						"Content-Type": "application/json",
						Authorization: "Bearer " + accessKey,
					},
					credentials: "include",
				}
			);

			const content = await response.json();
			// console.log(content);
			// console.log(content.data);
			updateUser(content.data);

			// console.log($user);
			// console.log('between');
			if (document.readyState && $user) {
				// console.log($user?.data_penduduk);
				// console.log('end');
				// if (complete) {
				// 	console.log('lengkap');
				$lengkap = true;
				// } else {
				// 	$lengkap = true;
				// 	console.log('tidak lengkap');
				// 	iconUserClick();
				// 	$lengkap = false;
				// }
			}
		}
	});
</script>

<div
	class="fixed top-0 left-0 right-0 flex z-30 justify-between h-10 w-full bg-sky-900 md:bg-opacity-60 px-0"
>
	<div class="w-1/3 px-2 md:px-10 flex items-center bg-sky-900">
		<img src={Logo} alt="logo" class="w-7" />
	</div>
	<div class="w-1/3 bg-sky-900 justify-center flex">
		<h1 class="text-xs font-semibold py-2 md:flex hidden text-white">
			Sistem Pengelolaan Gudang Berikat lestari berkah sae
		</h1>
	</div>
	<div class="w-1/3 bg-sky-900 flex items-center justify-end px-2 md:px-10">
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<div
			on:click={iconUserClick}
			class="bg-white cursor-pointer p-0.5 px-3 rounded-3xl flex"
		>
			<h1 class="text-gray-400 text-xs">{$user?.username}</h1>
			<div class="w-5 pt-0.5">
				<svg
					id="iconUser"
					class="transition"
					xmlns="http://www.w3.org/2000/svg"
					enable-background="new 0 0 1024 1024"
					viewBox="0 0 1024 1024"
					><path
						d="M670.1 278.4c0 8.8-.6 17.6-1.7 26.3.5-3.5 1-7.1 1.4-10.6-2.4 17.4-7 34.3-13.7 50.5 1.3-3.2 2.7-6.4 4-9.6-6.7 15.8-15.3 30.6-25.8 44.2 2.1-2.7 4.2-5.4 6.3-8.1-10.4 13.4-22.5 25.5-35.9 35.9 2.7-2.1 5.4-4.2 8.1-6.3-13.6 10.4-28.4 19.1-44.2 25.8 3.2-1.3 6.4-2.7 9.6-4-16.2 6.7-33.1 11.3-50.5 13.7 3.5-.5 7.1-1 10.6-1.4-17.5 2.3-35.1 2.3-52.6 0 3.5.5 7.1 1 10.6 1.4-17.4-2.4-34.3-7-50.5-13.7 3.2 1.3 6.4 2.7 9.6 4-15.8-6.7-30.6-15.3-44.2-25.8 2.7 2.1 5.4 4.2 8.1 6.3-13.4-10.4-25.5-22.5-35.9-35.9 2.1 2.7 4.2 5.4 6.3 8.1-10.4-13.6-19.1-28.4-25.8-44.2 1.3 3.2 2.7 6.4 4 9.6-6.7-16.2-11.3-33.1-13.7-50.5.5 3.5 1 7.1 1.4 10.6-2.3-17.5-2.3-35.1 0-52.6-.5 3.5-1 7.1-1.4 10.6 2.4-17.4 7-34.3 13.7-50.5-1.3 3.2-2.7 6.4-4 9.6 6.7-15.8 15.3-30.6 25.8-44.2-2.1 2.7-4.2 5.4-6.3 8.1 10.4-13.4 22.5-25.5 35.9-35.9-2.7 2.1-5.4 4.2-8.1 6.3 13.6-10.4 28.4-19.1 44.2-25.8-3.2 1.3-6.4 2.7-9.6 4 16.2-6.7 33.1-11.3 50.5-13.7-3.5.5-7.1 1-10.6 1.4 17.5-2.3 35.1-2.3 52.6 0-3.5-.5-7.1-1-10.6-1.4 17.4 2.4 34.3 7 50.5 13.7-3.2-1.3-6.4-2.7-9.6-4 15.8 6.7 30.6 15.3 44.2 25.8-2.7-2.1-5.4-4.2-8.1-6.3 13.4 10.4 25.5 22.5 35.9 35.9-2.1-2.7-4.2-5.4-6.3-8.1 10.4 13.6 19.1 28.4 25.8 44.2-1.3-3.2-2.7-6.4-4-9.6 6.7 16.2 11.3 33.1 13.7 50.5-.5-3.5-1-7.1-1.4-10.6C669.5 260.8 670 269.6 670.1 278.4c.1 20.9 18.3 41 40 40 21.6-1 40.1-17.6 40-40-.2-47.9-14.6-96.9-42.8-135.9-7.6-10.5-15.7-20.8-24.7-30.1-9.1-9.4-19.1-17.5-29.5-25.4-18.9-14.4-40-25-62.4-33.2-90.3-33.1-199.2-3.6-260.3 70.8-8.4 10.2-16.4 20.8-23.2 32.2-6.8 11.3-12.1 23.3-17 35.5-9.2 22.6-13.9 46.6-15.8 70.9-3.7 47.6 8.7 97.3 33.5 138.1 23.9 39.4 60 73.2 102.2 92.3 12.4 5.6 25.1 10.8 38.3 14.5 13.1 3.6 26.4 5.6 39.9 7.2 24.6 2.9 49.7.9 74-4 92.3-18.8 169.6-98.3 183.9-191.6 2.1-13.6 3.7-27.2 3.7-41 .1-20.9-18.5-41-40-40C688.3 239.4 670.1 256 670.1 278.4zM802.8 903.7c-19.6 0-39.2 0-58.8 0-46.7 0-93.3 0-140 0-56.2 0-112.4 0-168.7 0-48.5 0-97 0-145.6 0-22.7 0-45.4.2-68.1 0-2.5 0-5-.2-7.4-.5 3.5.5 7.1 1 10.6 1.4-4-.6-7.8-1.7-11.5-3.2 3.2 1.3 6.4 2.7 9.6 4-4-1.7-7.7-3.9-11.2-6.6 2.7 2.1 5.4 4.2 8.1 6.3-3-2.5-5.8-5.2-8.2-8.2 2.1 2.7 4.2 5.4 6.3 8.1-2.7-3.5-4.8-7.2-6.6-11.2 1.3 3.2 2.7 6.4 4 9.6-1.5-3.7-2.5-7.6-3.2-11.5.5 3.5 1 7.1 1.4 10.6-1.6-12.1-.5-24.9-.5-37.1 0-14.3 0-28.5 0-42.8 0-10.7.6-21.3 2-31.9-.5 3.5-1 7.1-1.4 10.6 2.8-20.5 8.2-40.6 16.3-59.7-1.3 3.2-2.7 6.4-4 9.6 7.8-18.2 17.8-35.3 29.9-51-2.1 2.7-4.2 5.4-6.3 8.1 12.1-15.5 26-29.5 41.6-41.6-2.7 2.1-5.4 4.2-8.1 6.3 15.7-12.1 32.8-22.1 51-29.9-3.2 1.3-6.4 2.7-9.6 4 19.1-8 39.1-13.5 59.7-16.3-3.5.5-7.1 1-10.6 1.4 14.8-1.9 29.5-2 44.4-2 18.3 0 36.6 0 54.9 0 42.7 0 85.4 0 128.1 0 16.5 0 32.9-.1 49.4 2-3.5-.5-7.1-1-10.6-1.4 20.5 2.8 40.6 8.2 59.7 16.3-3.2-1.3-6.4-2.7-9.6-4 18.2 7.8 35.3 17.8 51 29.9-2.7-2.1-5.4-4.2-8.1-6.3 15.5 12.1 29.5 26 41.6 41.6-2.1-2.7-4.2-5.4-6.3-8.1 12.1 15.7 22.1 32.8 29.9 51-1.3-3.2-2.7-6.4-4-9.6 8 19.1 13.5 39.1 16.3 59.7-.5-3.5-1-7.1-1.4-10.6 1.9 15.1 2 30.1 2 45.3 0 16.5 0 33 0 49.5 0 5.7.2 11.4-.5 17 .5-3.5 1-7.1 1.4-10.6-.6 4-1.7 7.8-3.2 11.5 1.3-3.2 2.7-6.4 4-9.6-1.7 4-3.9 7.7-6.6 11.2 2.1-2.7 4.2-5.4 6.3-8.1-2.5 3-5.2 5.8-8.2 8.2 2.7-2.1 5.4-4.2 8.1-6.3-3.5 2.7-7.2 4.8-11.2 6.6 3.2-1.3 6.4-2.7 9.6-4-3.7 1.5-7.6 2.5-11.5 3.2 3.5-.5 7.1-1 10.6-1.4C807.4 903.5 805.1 903.6 802.8 903.7c-10.3.1-20.9 4.4-28.3 11.7-6.9 6.9-12.2 18.3-11.7 28.3 1 21.4 17.6 40.3 40 40 38.9-.6 73.1-26 84.5-63.3 4.5-14.8 3.5-30.7 3.5-45.9 0-34.8 1.1-69.3-4.9-103.8-8.8-50.5-34.2-98-69-135.3-34.8-37.3-81.6-64.7-131.1-76.9-28.4-7-57-8.1-86-8.1-29.8 0-59.5 0-89.3 0-29.4 0-58.7 0-88.1 0-29.7 0-59.2 1.4-88.1 9.1-49.1 13-95.3 40.7-129.4 78.3-34.4 37.9-59.3 85.5-67.4 136.3-5.4 34.1-4.3 68.3-4.3 102.7 0 15.8-.9 32.3 4.8 47.4 7.4 19.4 19.2 34.7 36.5 46.2 13.5 8.9 30.6 13.2 46.6 13.4 7.8.1 15.6 0 23.4 0 20 0 39.9 0 59.9 0 28.4 0 56.7 0 85.1 0 33 0 66 0 99 0 33.9 0 67.7 0 101.6 0 31 0 61.9 0 92.9 0 24.3 0 48.6 0 72.8 0 13.9 0 27.8 0 41.7 0 1.8 0 3.6 0 5.4 0 20.9 0 41-18.4 40-40C841.9 922 825.3 903.7 802.8 903.7z"
					/></svg
				>
			</div>
		</div>
	</div>
</div>
