<script>
  import { getContext } from "svelte"
  const { styleable } = getContext("sdk")
  const component = getContext("component")
  export let dataProvider

  const addEmbed = (url) => {
    return url.replace('//music', '//embed.music')
  }

  $: lists = dataProvider?.rows?.map((obj) => ({
    name: obj.Name,
    url: addEmbed(obj.Url)
  })) ?? [];

  let currentPlay = addEmbed('https://music.apple.com/gb/playlist/peace-on-earth/pl.cc32b7d441a04269a559715bf9e0b90a')
</script>

<div use:styleable={$component.styles} class="container">
  <iframe allow="autoplay *; encrypted-media *;"
          frameborder="0"
          height="450"
          style="width:100%;
          max-width:660px;
          overflow:hidden;
          background:transparent;"
          sandbox="allow-forms
           allow-popups
           allow-same-origin
           allow-scripts
           allow-storage-access-by-user-activation
           allow-top-navigation-by-user-activation"
          src={currentPlay}>
  </iframe>
  <div class="buttonContainer">
    {#each lists as list (list)}
      {#if list.url && list.name}
          <button class="button" on:click={()=> currentPlay = list.url}>
            {list.name}
          </button>
      {/if}
    {/each}
  </div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: row;
    gap: 1rem;
  }

  .buttonContainer {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    padding-top: 1rem;
  }

  .button {
    background-color: rgb(226, 226, 228);
    border-style: none;
    padding: 0.5rem 1rem;
    border-radius: 1rem;
    transition: 100ms;
    font-weight: bold;
    color: #5b5b5b;
    box-shadow: 0 0.2rem 0 rgba(0, 0, 0, 0.1);
  }

  .button:hover {
    background-color: rgb(220, 220, 223);
  }

  .button:active {
    background-color: rgb(226, 226, 228);
  }

  .container {
    display: flex;
    flex-direction: row;
  }
</style>