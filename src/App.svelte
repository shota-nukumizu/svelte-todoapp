<script lang="ts">
	let title = ''

	// 作成ボタンを押したときの処理
	const handleClickCreateButton = () => {
		alert(title)
		title = ''
	}
</script>

<main>
	<label for="">
		タイトル
		<input bind:value={title} />
	</label>
	<button on:click={handleClickCreateButton}>作成</button>
</main>

<style>
</style>