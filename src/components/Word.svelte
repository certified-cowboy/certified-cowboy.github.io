<script>
  let word = null;

  const fetchWord = async () => {
    const res = await fetch('/data/words.json');
    const data = await res.json();
    word = data.data[Math.floor(Math.random() * data.data.length)];

  };

  fetchWord();
</script>

{#if word}
    <div class="bg-yellow-300 p-6 max-w-2xl w-full border-4 border-black retro-shadow">
        <h1 class="text-2xl text-center text-red-600 mb-4 break-words">{ word.w }</h1>
    {#if word.e}
        <div class="text-xs text-center text-gray-700 italic mb-6 break-words">{@html word.e}</div>
    {/if}

    {#if word.m.length > 0}
    <div class="border-t-2 border-black pt-4">
        <h2 class="text-lg text-indigo-700 mb-2">{word.m.length === 1 ? 'Význam' : 'Významy'}:</h2>
        <ul class="list-decimal list-inside space-y-4 text-sm text-black/90 break-words">
          {#each word.m as m}
            <li>
              {@html m.m}
              {#if m.e}
                <span class="text-gray-700 block mt-0.5 break-words">„{@html m.e}“</span>
              {/if}
            </li>
          {/each}
        </ul>
      </div>
    {/if}

    {#if word.i.length > 0}
      <div class="border-t-2 border-black pt-4 mt-4">
        <h2 class="text-lg text-pink-600 mb-2">Fráze a idiomy:</h2>
        <ul class="list-disc list-inside space-y-2 text-sm text-black/90 break-words">
          {#each word.i as i}
            <li>{@html i}</li>
          {/each}
        </ul>
      </div>
    {/if}

    {#if word.p.length > 0}
      <div class="border-t-2 border-black pt-4 mt-4">
        <h2 class="text-lg text-teal-700 mb-2">Přísloví, úsloví a pořekadla:</h2>
        <ul class="list-disc list-inside space-y-2 text-sm text-black/90 break-words">
          {#each word.p as p}
            <li>{@html p}</li>
          {/each}
        </ul>
      </div>
    {/if}
  </div>
{:else}
  <p>Loading...</p>
{/if}
