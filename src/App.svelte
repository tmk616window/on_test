<script lang="ts">
	export let text: string;
	export let counter: number;
  type content = {
    counter: number,
    text: string
  }
  let contents: content[] = [{counter: 0, text: "new"}];

  const sumText = (contents: content[]) => {
    let counterList: string[] = []
    for (let i = 0; i < contents.length; ++i) {
      counterList.push(contents[i].text)
    }
    return counterList
  }

  const sumCounter = (contents: content[]) => {
    return contents.reduce((sum, i) => sum + i.counter, 0);
  }

  const addContent = () => {
    contents = [...contents, {counter: 0, text: "new"}];
  };

  const removeContent = (id: number) => {
    contents = contents.filter((_, i) => i !== id)
  };

	const handleAddCounter = (index: number) => {
		contents[index].counter += 1;
	}

	const handleRemoveCounter = (index: number) => {
    if (contents[index].counter > 0) {
		  contents[index].counter -= 1;
    }
  }

	const handleResetCounter = (index: number) => {
		contents[index].counter = 0;
	}
</script>

<main>
  <h1>Multiple Counter</h1>
  {#each contents as content, index}
    <div key={index} id={index}>
      <input bind:value={contents[index].text} class="coutner-content">
      <div>
        {contents[index].counter}
        <button on:click={() => handleAddCounter(index)}>
          +
        </button>
        <button on:click={() => handleRemoveCounter(index)}>
          −
        </button>
        <button on:click={() => handleResetCounter(index)}>
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
    <p>title list:{sumText(contents)}</p>
    <p>{sumCounter(contents)}</p>
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

	.coutner-content {
    float: left;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>