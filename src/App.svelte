<script lang="ts">
  type content = {
    counter: number,
    title: string
  }
  let contents: content[] = [{counter: 0, title: "new"}];

  const sumTitle = (contents: content[]) => {
    const counterList: string[] = []
    for (let i = 0; i < contents.length; ++i) {
      if (contents[i].title != "") {
        counterList.push(contents[i].title)
      }
    }
    return counterList
  }

  const sumCounter = (contents: content[]) => {
    return contents.reduce((sum, i) => sum + i.counter, 0);
  }

  const addContent = () => {
    contents = [...contents, {counter: 0, title: "new"}];
  };

  const removeContent = (index: number) => {
    contents = contents.filter((_, i) => i !== index)
  };

	const addCounter = (index: number) => {
		contents[index].counter += 1;
	}

	const removeCounter = (index: number) => {
    if (contents[index].counter > 0) {
		  contents[index].counter -= 1;
    }
  }

	const resetCounter = (index: number) => {
		contents[index].counter = 0;
	}
</script>

<main>
  <h1>Multiple Counter</h1>
  {#each contents as content, index}
    <div id={index} class="content">
      <input bind:value={contents[index].title} class="title-input item">
      <div class="item">
        {contents[index].counter}
        <button on:click={() => addCounter(index)} class="btn btn--orange">
          +
        </button>
        <button on:click={() => removeCounter(index)} class="btn btn--blue">
          −
        </button>
        <button on:click={() => resetCounter(index)} class="btn btn--green">
          0
        </button>
        <button on:click={() => removeContent(index)}>
          ×
        </button>
      </div>
    </div>
  {/each}
  <br/>
  <button on:click={addContent}>new counter</button>
  <div>
    <p>title list: {sumTitle(contents)}</p>
    <p>sum of count: {sumCounter(contents)}</p>
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
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

  .btn--orange{
    color: #fff;
    background-color: #eb6100;
  }

  .btn--blue{
    color: #fff;
    background-color: blue;
  }

  .btn--green{
    color: #fff;
    background-color: green;
  }

  .content {
    display: flex;
    flex-wrap: wrap;
    width: 300px;
    margin:0 auto;
  }

  .item {
    width: 150px;
  }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>