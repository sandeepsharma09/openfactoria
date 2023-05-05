<script>
// @ts-nocheck

import localforage from 'https://esm.run/localforage';
import Nav from './lib/Nav.svelte'
let db = localforage.createInstance({ name: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJkaWQ6ZXRocjoweEM2NUZkOEY2NkRlRDJCZTZkRWM0RDVGNjg3NDAwMzI0RmQyRTdmYkYiLCJpc3MiOiJuZnQtc3RvcmFnZSIsImlhdCI6MTY4MzIxMzI0NTk5OSwibmFtZSI6InRlc3QifQ.1K4D3ZRCJKanOuDfUeXEllRFHQqazCwk_BdACNCsT64" })
let key = "";
let disabled;
db.getItem("key").then((_key) => {
  key = _key
})
const save = async () => {
  await db.setItem("key", key)
  disabled = true
}
</script>
<Nav config={"selected"} />
<div class='top'>
<form class='form' on:submit|preventDefault|stopPropagation={save}>
  <div class='item'>
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>NFT.STORAGE API KEY</label>
    {#if disabled}
      <input disabled type='text' placeholder="NFT.STORAGE key" bind:value={key}>
    {:else}
      <input type='text' placeholder="NFT.STORAGE key" bind:value={key}>
    {/if}
  </div>
  <div class='item'>
    {#if disabled}
      <div class='btn disabled'>saved</div>
    {:else}
      <input type='submit' value="save" />
      <br><br>
      <div class='description'>You can get a free API key at <a href="https://nft.storage">https://nft.storage</a></div>
    {/if}
  </div>
</form>
</div>
<style>
.description {
  padding: 10px 0;
  text-transform: lowercase;
}
.description a {
  color: royalblue;
  text-decoration: none;
}
.form {
  margin: 0;
  border: none;
  padding: 0;
}
input[type=text] {
  border: 2px solid #eaeaea;
}
.disabled {
  background: gray;
}
</style>
