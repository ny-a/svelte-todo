<script>
    let todos = [
        { id: 0, done: false, text: "Sample Todo" },
    ];
    let text = "";

    $: nextId = Math.max(...todos.map(i => i.id)) + 1;

    function addTodo() {
        const newTodo = { id: nextId, done: false, text: text };
        todos = [...todos, newTodo];
        text = "";
    }

    function toggleDoneStatus(id) {
        todos = todos.map(i => {
            if (i.id === id) {
                return {
                    id: i.id,
                    done: !i.done,
                    text: i.text,
                }
            } else {
                return i
            }
        })
    }
</script>

<main>
	<h1>TODO List</h1>

    <input bind:value={text} />
    <button on:click={addTodo}>Add</button>

    <div class="todoContainer">
        <ul>
            {#each todos as todo}
                <li on:click={toggleDoneStatus(todo.id)}>
                    {#if todo.done}
                        <s>{todo.text}</s>
                    {:else}
                        {todo.text}
                    {/if}
                </li>
            {/each}
        </ul>
    </div>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

    .todoContainer {
        margin: 0 auto;
        max-width: 400px;
    }

    ul {
        text-align: left;
    }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
