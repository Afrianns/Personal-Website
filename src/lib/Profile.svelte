<script lang="ts">
  // My Image
  import photo from "../assets/my-photo.png";
  // My Icon Links
  import Twitter from "../assets/link-img/twitter.svelte";
  import Linkedin from "../assets/link-img/linkedin.svelte";
  import Codewars from "../assets/link-img/codewars.svelte";
  import Github from "../assets/link-img/github.svelte";
  import FEMentor from "../assets/link-img/FEMentor.svelte";
</script>

<section class="content-wrapper wrapper">
  <div class="bio-wrapper-noicon">
    <div class="bio-info">
      <div class="bio-header">
        <p><span class="greet">HELLO</span>, MY NAME IS</p>
        <h1 class='brand'>HANIF NANDA AFRIAN</h1>
      </div>
      <p class="bio-desc">
        A Person who Love Web Programming especally Frontend and Love to
        Illustrate and Design, Always Curious About new Technology and Design.
      </p>

      <!-- <button>
        <span class="download"
          ><svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            ><path d="M5 20h14v-2H5v2zM19 9h-4V3H9v6H5l7 7l7-7z" /></svg
          ></span
        > Download CV</button
      > -->
      <ul class="link-icon">
        <li>
          <a href="https://www.linkedin.com/in/hanif-nanda-afrian-203788254/">
            <Linkedin />
          </a>
        </li>
        <li>
          <a href="https://twitter.com/Afrianku">
            <Twitter />
          </a>
        </li>
        <li>
          <a href="https://github.com/Afrianns">
            <Github />
          </a>
        </li>
        <li>
          <a href="https://www.codewars.com/users/HanzN">
            <Codewars />
          </a>
        </li>
        <li>
          <a href="https://www.frontendmentor.io/profile/HanzN77">
            <FEMentor />
          </a>
        </li>
      </ul>
    </div>
  </div>
</section>

<style>
  .greet {
    color: var(--secondary);
  }

  .bio-info {
    filter: saturate(0.5);
  }

  .bio-header {
    margin: 3rem 0 0;
  }
  .bio-header p {
    font-size: 1.5rem;
  }

  .bio-info h1 {
    font-family: var(--font-brand);
    font-size: 4rem;
    letter-spacing: 1px;
    padding: 0;
    margin-bottom: 2rem;
    line-height: 5rem;
  }

  .bio-info .bio-desc {
    color: grey;
    font-weight: 400;
    max-width: 45ch;
    margin: auto;
    text-transform: lowercase;
  }

  .link-icon {
    margin: 3rem 0;
    align-items: center;
    justify-content: center;
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  .link-icon > * {
    cursor: pointer;
    margin: 0 0 2rem;
  }

  @media screen and (max-width: 600px) {
    .content-wrapper {
      margin: 2rem;
      display: block;
    }

    .bio-info {
      margin: 0;
    }

    .bio-info .bio-desc{
      margin: 1rem auto;
    }
    

    .link-icon > * {
      margin: 0 0 0.5rem;
    }

    .bio-header h1 {
      font-size: 3rem;
      line-height: 5rem;
    }
  }

  @media screen and (max-width: 400px) {
    .content-wrapper {
      margin: 1rem;
    }
    .bio-wrapper-noicon .bio-info {
      text-align: center;
    }
    .bio-info button {
      width: 100%;
    }

    .link-icon {
      gap: 3rem;
    }
  }
</style>
