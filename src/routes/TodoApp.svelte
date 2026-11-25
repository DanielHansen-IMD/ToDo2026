<script>
    let todoItem = $state('');
    let todoList = $state([]);

    function addItem(event) {
        // prevent form submission from destroying page
        event.preventDefault();

        // 'adding' the todoItem to todoList
        todoList = [...todoList, {
            text: todoItem,
            done: false
        }];

        // clear todoItem
        todoItem = '';
    }
    //$inspect(todoList);

    function removeItem(index) {
        // remove the identified item from the todoList
        todoList.splice(index,1);
    }

</script>


<form onsubmit={addItem}>
    <input type="text" name="todo-item" id="todo-item" bind:value={todoItem} >
    <button type="submit">Add Item</button>
</form>

<div class="todo-list">
    <ul>
        {#each todoList as item, index}
            <li>
                <input type="checkbox" bind:checked={item.done}>
                <span class:done={item.done}>{item.text}</span>
                <button type="button" onclick={() => removeItem(index)}>x</button>
            </li>
        {/each}
    </ul>
</div>

<style>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
    .done {
        color: grey;
        text-decoration: line-through;
    }
</style>