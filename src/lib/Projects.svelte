<script lang="ts">
  import Border from "../assets/icons/border.svelte";
  import Placeholder from "../assets/blank-profile.png";
  import axios from "axios";
  let url = "https://api.netlify.com/api/v1/sites";
  let isLoad = false;

  let api_key = import.meta.env.VITE_API_ACCESS;
  async function get_project(url) {
    return axios.get(url, {
      headers: {
        Authorization: `Bearer ${api_key}`,
      },
    });
  }
  let result = get_project(url + "?per_page=6");

  function loadMore() {
    let param = "";
    if (isLoad) {
      param = "?per_page=6";
    }
    result = get_project("https://api.netlify.com/api/v1/sites" + param);
    isLoad = !isLoad;
  }
</script>

<section class="main" id="projects">
  <h1>PROJECTS</h1>
  <Border />

  {#await result}
    <p>Loading</p>
  {:then sites}
    <div class="list-projects">
      {#each sites.data as site}
        <div class="projects">
          <div class="img-container">
            <img
              src={site["screenshot_url"] || Placeholder}
              class="placeholder"
              alt=""
            />
          </div>
          <h1>{site["name"].split("-").join(" ")}</h1>
          <a class="link" href={site["url"]} target="_blank">visit website</a>
        </div>
      {/each}
    </div>
    <button on:click={loadMore}>
      {#if isLoad}
        Close Projects
      {:else}
        Load Projects
      {/if}
      <span class="download">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          ><path
            d="m11.293 17.293 1.414 1.414L19.414 12l-6.707-6.707-1.414 1.414L15.586 11H6v2h9.586z"
          /></svg
        >
      </span></button
    >
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</section>

<style>
  button {
    margin: auto;
  }
  .list-projects {
    margin: 4rem 0;
    display: grid;
    justify-content: center;
    gap: 1.5rem;
    font-size: 1rem;
    grid-template-columns: repeat(3, max-content);
  }
  .placeholder {
    object-fit: contain;
    width: 20rem;
    transition: all 0.5s ease;
    height: 15rem;
  }

  .placeholder:hover {
    filter: brightness(0.5);
    transform: scale(1.2);
  }

  .placeholder::after {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100px;
    height: 100px;
    background-color: red;
  }

  .img-container {
    background-color: var(--secondary-bg);
    overflow: hidden;
    padding: 2px;
  }

  .img-container:hover {
    border: 2px solid var(--secondary);
    padding: 0;
  }

  .projects {
    cursor: pointer;
    margin: 2rem 0;
  }
  .projects h1 {
    font-family: var(--font-epi);
    padding: 0.75rem 0;
    text-align: left;
  }
  .projects .link {
    color: var(--secondary);
    display: block;
    text-align: right;
    font-family: var(--font-epi);
  }
</style>
