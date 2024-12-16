<script>
    let catImage = '';
    let catFact = '';
  
    async function fetchCatData() {
      try {
        const imageResponse = 
        await fetch('https://api.thecatapi.com/v1/images/search');

        const imageData = await imageResponse.json();
        catImage = imageData[0]?.url || 'No image found';

        const factResponse = 
        await fetch('https://catfact.ninja/fact');

        const factData = await factResponse.json();
        catFact = factData.fact || 'No fact found';

      } catch (error) {
        console.error('Error fetching cat data:', error);
        catImage = '';
        catFact = 'Error loading cat fact.';
      }
    }
</script>
  
  <div class="cat-container">
    <button on:click={fetchCatData}>Show Me a Cat!</button>
    {#if catImage}
      <img src={catImage} alt="Random Cat" />
    {/if}
    {#if catFact}
      <p><strong>Cat Fact:</strong> {catFact}</p>
    {/if}
  </div>
  