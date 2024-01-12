<script>
      import { Peer } from 'peerjs';
  import { onMount } from 'svelte';
  import { createEventDispatcher } from 'svelte';
      let username = "";
  let password = "";
  let NO_ID = "";
</script>
<style>
    form {
      max-width: 400px;
      margin: auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
  
    label {
      display: block;
      margin-bottom: 10px;
    }
  
    input {
      width: 100%;
      padding: 8px;
      margin-bottom: 10px;
      box-sizing: border-box;
    }
  
    button {
      background-color: #4caf50;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  
    button:hover {
      background-color: #45a049;
    }
  </style>
  <form>
    <label>
      Username:
      <input type="text" bind:value={username} name="username">
    </label>
  
    <label>
      Password:
      <input type="password" bind:value={password} name="password">
    </label>
  
    <label>
      ID:
      <input type="text" bind:value={NO_ID} name="id">
    </label>
  </form>
  <p>Username: {username}</p>
  <p>Password: {password}</p>
  <p>ID: {NO_ID}</p>