<script lang="ts">
  import Css from "../assets/skill-icons/css.svelte";
  import Html from "../assets/skill-icons/html.svelte";
  import Sass from "../assets/skill-icons/sass.svelte";
  import Javascript from "../assets/skill-icons/javascript.svelte";
  import Vue from "../assets/skill-icons/vue.svelte";
  import Laravel from "../assets/skill-icons/laravel.svelte";

</script>

<section class="main" id="skills">
  <h1 class="text-header">SKILLS</h1>
  <div class="list-skills">
    <p><Html /> HTML</p>
    <p><Css /> CSS</p>
    <p><Javascript /> JavaScript</p>
    <p><Laravel /> Laravel</p>
    <p><Sass /> SASS</p>
    <p><Vue /> Vue</p>
  </div>
</section>

<style>
  .main {
    background-color: var(--secondary-bg);
  }
  #skills {
    position: relative;
  }

  #skills::after {
    content: "";
    position: absolute;

    right: -7.5rem;
    transform: rotate(4deg);
    bottom: 0;
    width: 50rem;
    height: 20rem;
    background-repeat: no-repeat;
    object-fit: cover;
    background-size: contain;
    background-position: bottom right;
    z-index: 0;
    background-image: url("../assets/icons/decoration-two.svg");
  }

  .list-skills {
    z-index: 2;
    position: relative;
    max-width: 70vw;
    margin: 2rem auto 3rem;
    justify-content: center;
    display: grid;
    grid-template-columns: repeat(3, max-content);
    gap: 2rem;
    font-family: var(--font-epi);
  }
  .list-skills > * {
    transition: all 0.5s ease-in;
    display: flex;
    align-items: center;
    gap: 10px;
    justify-self: start;
    background-color: var(--bg);
    padding: 2rem 2.5rem;
    width: 100%;
    max-width: 20rem;
    cursor: pointer;
    box-shadow: 1px 10px 20px rgba(32, 32, 32, 0.02);
    border-radius: 10px;
  }

  .list-skills p {
    align-content: end;
    column-gap: 1rem;
    border: 2px solid transparent;
  }

  .list-skills p:hover {
    border: 2px solid var(--secondary);
  }

  @media screen and (max-width: 1055px) {
    .list-skills {
      margin-left: 1rem;
      margin-right: 1rem;
      max-width: 100vw;
      grid-template-columns: repeat(2, max-content);
    }
  }

  @media screen and (max-width: 700px) {
    .list-skills {
      grid-template-columns: 1fr;
      font-size: 1.5rem;
    }

    .list-skills > * {
      justify-content: center;
      justify-self: center;
    }
  }
</style>
