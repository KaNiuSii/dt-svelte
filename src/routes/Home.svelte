<script>
  import { navigate } from 'svelte-routing';

  function goToLearn() {
    navigate('dt-svelte/learn');
  }

  function goToTest() {
    navigate('dt-svelte/test');
  }
</script>

<style>
  :global(body, html) {
			height: 100%;
			margin: 0;
			font-family: Arial, sans-serif;
			background-color: #006d40;
			color: white;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
		}
  img {
    display: block;
    margin: auto;
  }

  .container {
    width: 80%;
    max-width: 1200px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .panel {
    width: 45%;
    background-color: #00895c;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    text-align: center;
    transition: 0.3s;
  }

  .panel:hover {
    box-shadow: 0 16px 32px 0 rgba(0,0,0,0.2);
  }

  .button {
    background-color: #2e9d32;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s ease;
    transition: color 0.3s ease;
  }

  .button:hover {
    background-color: #66db6a;
    color: black;
  }

  h2 {    
    margin-bottom: 30px;    
  }

  .icon {
    font-size: 40px;
    margin-bottom: 15px;
  }

  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
  }
</style>

<div class="content">
  <img src="https://raw.githubusercontent.com/KaNiuSii/design-thinking-eco/main/bg.png" alt="Image of a tree">
  <br>
  <div class="container">
    <div class="panel">
      <h2>Nauka</h2>
      <span class="icon">&#x1F4DA;</span> <!-- Book emoji -->
      <p>Odkryj nową wiedzę i umiejętności dzięki interaktywnym lekcjom i materiałom.</p>
      <button class="button" on:click={goToLearn}>Nauka</button>
    </div>
    
    <div class="panel">
      <h2>Test</h2>
      <span class="icon">&#x1F3C6;</span> <!-- Trophy emoji -->
      <p>Rzuć wyzwanie swojemu zrozumieniu i zastosuj to, czego się nauczyłeś w praktycznym kontekście.</p>
      <button class="button" on:click={goToTest}>Test</button>
    </div>
  </div>
  
</div>