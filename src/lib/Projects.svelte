<script lang="ts">
  import Placeholder from "../assets/blank-image.png";
  import LoadingIcon from "../assets/icons/loading.svelte";
  import axios from "axios";
  import { onMount } from "svelte";
  
  let url = "https://api.netlify.com/api/v1/sites";
  let isLoad = false;
  
  let sites = [];
  let num = 0;
  let isLoadedAll = false;
  let Loading = false;
  let LoadingMore = false;
  let total_sites = 0;
  let error = '';

  const api_key = import.meta.env.VITE_API_ACCESS;

  async function get_project(url, param) {
    await axios.get(url + param, {
      timeout: 10000,
      headers: {
        Authorization: `Bearer ${api_key}`,
      },
    }).then(result => {
      num++;
      if(param == ''){
        // result of total sites from user
        total_sites = result.data[0]['site_count'];
      } else{
        // result of every site & push it to sites
        result.data.forEach(element => {
          sites = [...sites, element];
        });
        // loading boolean 
        Loading = false;
        LoadingMore = false;
      }
    }).catch(er => {
      error = er.message;
      console.log(er.message);
    })
  }

  // init Load & for error if occurs
  function initLoad() {
    Loading = true;
    error = '';
    getUser();
    get_project(url, "?page=1&per_page=6");
  }

  function loadMore() {
    // click more pagination
    error = '';
    LoadingMore = true;
    let param =  `?page=${num}&per_page=6`;
    get_project("https://api.netlify.com/api/v1/sites", param);
    // calculate total side to determined load more
    let calc = total_sites - (num * 6);
    // console.log(total_sites, sites.length, calc);
    if(calc <= 0){
      isLoadedAll = true;
    }
  }

  // get user & get total sites
  function getUser(){
    get_project("https://api.netlify.com/api/v1/users", '');
  }
  
  // convert timedate
  function converDate(date) {
    let newdate = new Date(date);
    let arrayUTC = newdate.toUTCString().split(" ");
    let res = arrayUTC.filter((_, i) => i <= 3);
    return res.join(" ");
  }
  
  // Load first time
  onMount(() => {
    initLoad();
  })
</script>

<section class="main" id="projects">
  <h1 class="text-header">PROJECTS</h1>
  {#if Loading && !error}
      <LoadingIcon/>
  {:else if error && Loading}
      <div class="error-wrapper">
        <p class="error">{error}</p>  
        <p class='info'>Check your internet and <span class="loadmore" on:keypress={initLoad} role="button" tabindex="0" on:click={initLoad}>Reload</span></p>
      </div>
  {:else}
      <div class="list-projects">
        {#each sites as site}
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
              <h1 class="subtitle">{site["name"].split("-").join(" ")}</h1>
              <a class="link" href={site["url"]} target="_blank">visit site</a>
            </div>
          </div>
        {/each}
      </div>
      {#if LoadingMore && !error}
        <LoadingIcon/> 
      {:else if error && LoadingMore}
      <div class="error-wrapper">
        <p class="error">{error}</p>  
        <p class='info'>Check your internet and <span class="loadmore" on:keypress={loadMore} role="button" tabindex="0" on:click={loadMore}>Reload</span></p>
      </div>
      {:else}
        {#if !isLoadedAll && !Loading}
          <button class="button-style" on:click={loadMore}>
            Load More
            <span class="download">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                class={isLoad ? "rotate" : ""}
                viewBox="0 0 24 24"
                ><path
                  d="m11.293 17.293 1.414 1.414L19.414 12l-6.707-6.707-1.414 1.414L15.586 11H6v2h9.586z"
                /></svg
              >
            </span>
          </button>
          {/if}
      {/if}
    {/if}
</section>

<style>

  .error-wrapper{
    font-family: var(--font-secondary);
    margin-top:5rem;
    line-height: 0;
    text-transform: uppercase;
  }
  .error{
    font-size: 1.5rem;
    font-style: italic;
    color: red;
    margin: 2rem;
  }

  .info{
    line-height: 0;
    font-size: 1rem;
    font-weight: 400;
    color: rgb(234, 232, 232);
  }

  .loadmore{
    cursor: pointer;
    color: aqua;
  }

  .loadmore:hover{
    text-decoration: underline;
  }

 .main {
    background-color: var(--secondary-bg);
    padding-bottom: 4rem;
  }
  
  .rotate {
    transform: rotate(180deg);
  }

  .subtitle{
    font-size: 1rem;
  }

  .button-style {
    margin: auto;
    transition: all 0.5s ease-in-out;
    transform: translateX(0);
  }
  
  .button-style:hover svg {
    transform: translateX(5px);
  }

  .list-projects {
    margin: 2rem 0 3rem;
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

  .projects:hover .placeholder {
    filter: brightness(0.5);
    transform: scale(1.1);
  }

  .img-container {
    background-color: var(--secondary-bg);
    overflow: hidden;
    padding: 2px;
    border-radius: 10px 10px 0 0;
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

  .projects {
    border: 2px solid transparent;
    border-radius: 10px;
    cursor: pointer;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.005);
    background-color: var(--tertiery-bg);
  }
  
  .projects:hover {
    border: 2px solid var(--secondary);
    padding: 0;
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
    font-family: var(--font-secondary);
    padding: 0.75rem 0 2rem;
    text-align: left;
    text-transform: uppercase;
  }
  .projects .link {
    color: var(--secondary);
    display: block;
    text-align: right;
    font-size: .9rem;
    font-family: var(--font-secondary);
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
