<script lang="ts">
  import Border from "../assets/icons/border.svelte";
</script>

<section class="main" id="skills">
  <h1 class='text-header'>SKILLS</h1>
  <Border />
  <div class="list-skills">
    <p><span class="lists" /> HTML</p>
    <p><span class="lists" /> CSS</p>
    <p><span class="lists" /> JavaScript</p>
    <p><span class="lists" /> PHP</p>
    <p><span class="lists" /> SASS</p>
    <p><span class="lists" /> Vue</p>
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
    /* bottom: 10%; */

    right: -7.5rem;
    transform: rotate(4deg);
    bottom: 0;
    width: 50rem;
    height: 20rem;
    background-repeat: no-repeat;
    object-fit: cover;
    background-size: contain;
    background-position: bottom right;
    background-image: url("../assets/icons/decoration-two.svg");
  }

  .list-skills {
    max-width: 70vw;
    margin: 5rem auto 3rem;
    justify-content: space-around;
    display: grid;
    grid-template-columns: repeat(3, max-content);
    row-gap: 3rem;
    font-family: var(--font-epi);
  }
  .list-skills > * {
    display: flex;
    align-items: center;
    gap: 10px;
    justify-self: start;
  }
  .lists {
    width: 10px;
    height: 15px;
    background-color: var(--secondary);
  }

  @media screen and (max-width: 1055px) {
    .list-skills {
      max-width: 100vw;
    }
  }

  @media screen and (max-width: 600px) {
    .list-skills {
      grid-template-columns: repeat(2, max-content);
      font-size: 1.5rem;
    }
  }
</style>
