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
        <p><span class="greet">HI</span>, MY NAME IS</p>
        <h1><span class="nickname">HANIF</span> NANDA AFRIAN</h1>
      </div>
      <p class="bio-desc">
        A Person Who Love Web Programming especally Frontend and Love to
        Illustrate and Design, Always Curious About new Technology and Design.
      </p>
      <button>
        <span class="download"
          ><svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            ><path d="M5 20h14v-2H5v2zM19 9h-4V3H9v6H5l7 7l7-7z" /></svg
          ></span
        > Download CV</button
      >
    </div>
    <img class="my-photo" src={photo} alt="" />
  </div>
  <ul class="link-icon">
    <li class="test"><Linkedin /></li>
    <li><Twitter /></li>
    <li><Github /></li>
    <li><Codewars /></li>
    <li><FEMentor /></li>
  </ul>
</section>

<style>
  .nickname {
    border-bottom: 5px solid var(--secondary);
  }

  .greet {
    color: var(--secondary);
  }
  .bio-wrapper-noicon {
    justify-content: space-between;
    display: flex;
  }
  .content-wrapper {
    font-family: var(--font-fjall);
    /* margin-top: ; */
    margin: 3rem auto;
    display: flex;
    gap: 3rem;
    justify-content: center;
  }

  .bio-info {
    filter: saturate(0.5);
    text-align: left;
  }

  .bio-header {
    margin: 3rem 0;
  }
  .bio-header p {
    font-size: 1.5rem;
  }

  .bio-info h1 {
    font-size: 4rem;
  }

  .bio-info .bio-desc {
    color: grey;
    font-weight: 400;
    max-width: 45ch;
  }

  .link-icon {
    list-style: none;
  }
  .link-icon > * {
    cursor: pointer;
    margin: 0 0 2rem;
  }

  .my-photo {
    object-fit: cover;
    border-left: 2px solid var(--secondary);
  }



  @media screen and (max-width: 1055px) {
    .content-wrapper {
      margin: 3rem;
      flex-direction: column;
    }
    .link-icon {
      margin: 2rem 0;
      display: flex;
      gap: 3rem;
      justify-content: center;
    }
    .my-photo {
      max-width: 45%;
    }
    .bio-info {
      margin-right: -5.5rem;
    }
  }

  @media screen and (max-width: 600px) {
    .bio-wrapper-noicon {
      flex-direction: column-reverse;
    }

    .my-photo {
      margin: auto;
      max-width: 100%;
    }

    .bio-info {
      margin: 0;
    }

    .link-icon {
      flex-wrap: wrap;
    }

    .bio-header p {
      margin: 0 0 2rem;
    }

    .bio-header h1 {
      font-size: 3rem;
    }
  }
</style>
