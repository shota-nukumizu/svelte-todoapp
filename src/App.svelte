<script lang="ts">
  import { slide } from 'svelte/transition'

  type TodoItem = {
	id: number;
	title: string;
  }

  let title = '';
  let todoList: TodoItem[] = [];

  $: disabledCreateButton = title === '';

  // 作成ボタンを押したときの処理
  const handleClickCreateButton = () => {
	const id = new Date().getTime(); 
    todoList = [...todoList, { id, title }];
    title = '';
  };

  // 完了処理
  const completeItem = (index) => {
    todoList = todoList.filter((_, i) => i !== index);
  };
</script>

<main>
	<div class="container mt-3">
		<div class="row justify-content-center">
			<div class="col-lg-6 col-md-8">
			<h2>TODO アプリ</h2>
			<form>
				<div class="form-group">
				<label for="title">タイトル</label>
				<input id="title" class="form-control" bind:value={title} />
				</div>
				<div class="form-group text-center">
				<button
					class="btn btn-primary px-5"
					disabled={disabledCreateButton}
					on:click={handleClickCreateButton}>
					作成
				</button>
				</div>
			</form>
			</div>
		</div>
		<div class="row justify-content-center">
			<div class="col-lg-6 col-md-8">
			{#if todoList.length === 0}
				<div>アイテムを作成してください</div>
			{:else}
				<ul class="list-group">
				{#each todoList as todoItem, index (todoItem.id)}
					<li transition:slide class="list-group-item align-middle">
					{todoItem}
					<button
						class="btn btn-sm btn-success float-right"
						on:click={() => completeItem(index)}>
						×
					</button>
					</li>
				{/each}
				</ul>
			{/if}
			</div>
		</div>
	</div>
</main>