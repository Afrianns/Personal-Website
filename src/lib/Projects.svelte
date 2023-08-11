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

  result.then((r) => {
    console.log(r);
  });

  function loadMore() {
    let param = "";
    if (isLoad) {
      param = "?per_page=6";
    }
    result = get_project("https://api.netlify.com/api/v1/sites" + param);
    isLoad = !isLoad;
  }

  function converDate(date) {
    let newdate = new Date(date);
    let arrayUTC = newdate.toUTCString().split(" ");
    let res = arrayUTC.filter((_, i) => i <= 3);
    return res.join(" ");
  }
</script>

<section class="main" id="projects">
  <h1 class="text-header">PROJECTS</h1>
  <Border />

  {#await result}
    <p>Loading</p>
  {:then sites}
    <div class="list-projects">
      {#each sites.data as site}
        <div class="projects">
          <div class="img-container">
            <span class="date">{converDate(site["created_at"])}</span>
            <img
              src={site["screenshot_url"] || Placeholder}
              class="placeholder"
              alt=""
            />
          </div>
          <div class="context">
            <h1>{site["name"].split("-").join(" ")}</h1>
            <a class="link" href={site["url"]} target="_blank">visit website</a>
          </div>
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
    margin: 5rem 0 3rem;
    display: grid;
    justify-content: center;
    gap: 1.5rem;
    font-size: 1rem;
    grid-template-columns: repeat(3, max-content);
  }
  .placeholder {
    object-fit: cover;
    width: 20rem;
    transition: all 0.5s ease;
    height: 15rem;
  }

  .placeholder:hover {
    filter: brightness(0.5);
    transform: scale(1.2);
  }

  .img-container {
    background-color: var(--secondary-bg);
    border-radius: 10px;
    overflow: hidden;
    padding: 2px;
    position: relative;
  }

  .img-container::before {
    content: "";
    position: absolute;
    z-index: 5;
    top: -2rem;
    left: -5rem;
    bottom: 5px;
    width: 100vw;
    height: 50px;
    filter: blur(25px);
    background-color: rgb(28, 28, 28);
  }

  .img-container:hover {
    border: 2px solid var(--secondary);
    padding: 0;
  }

  .projects {
    border-radius: 10px;
    cursor: pointer;
    background-color: var(--tertiery-bg);
  }
  .context {
    padding: 0 15px 15px;
  }

  .date {
    margin: 1rem;
    position: absolute;
    padding: 5px 10px;
    right: 0;
    z-index: 5;
    box-shadow: 1px 1px 20px rgba(0, 0, 0, 0.556);
    background-color: var(--tertiery-bg);
    border-radius: 5px;
    color: var(--secondary);
  }
  .projects h1 {
    font-family: var(--font-alerta);
    padding: 0.75rem 0 2rem;
    text-align: left;
    text-transform: uppercase;
  }
  .projects .link {
    color: var(--secondary);
    display: block;
    text-align: right;
    font-family: var(--font-epi);
  }

  @media screen and (max-width: 1055px) {
    .list-projects {
      grid-template-columns: repeat(2, max-content);
    }
  }

  @media screen and (max-width: 700px) {
    .list-projects {
      grid-template-columns: max-content;
    }
  }
</style>
