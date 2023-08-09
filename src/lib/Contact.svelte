<script lang="ts">
</script>

<section class="main" id="contact">
  <div class="footer-wrapper">
    <div class="contact-wrapper">
      <h1 class="text-header">Contact</h1>
      <a href="#header" class="backToTop"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          ><path
            d="m12 3.879-7.061 7.06 2.122 2.122L12 8.121l4.939 4.94 2.122-2.122z"
          /><path
            d="m4.939 17.939 2.122 2.122L12 15.121l4.939 4.94 2.122-2.122L12 10.879z"
          /></svg
        ></a
      >
    </div>
    <div class="form-wrapper">
      <div class="left-wrapper">
        <label for="name">Name</label>
        <input type="text" name="name" id="name" />
        <label for="email">Email</label>
        <input type="text" name="email" id="email" />
      </div>
      <div class="right-wrapper">
        <label for="message">Message</label>
        <textarea name="message" id="message" cols="50" rows="50" />
        <button class="btn">
          Send
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
      </div>
    </div>
  </div>
</section>

<style>
  #contact {
    background-color: var(--tertiery-bg);
    padding: 2rem 0;
    margin-top: 1rem;
    border-right: 2px solid var(--secondary);
    position: relative;
  }
  #contact::after {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0;
    width: 50rem;
    height: 20rem;
    background-repeat: no-repeat;
    object-fit: cover;
    background-size: contain;
    background-position: bottom left;
    background-image: url("../assets/icons/decoration.svg");
  }

  .main {
    margin: 2rem auto 0;
  }

  .footer-wrapper {
    padding: 2rem;
    text-align: left;
    min-width: 75vw;
    margin: auto;
  }
  .footer-wrapper h1 {
    grid-area: 1;
  }

  .contact-wrapper {
    display: flex;
    max-width: 55rem;
    margin: auto;
    justify-content: space-between;
  }

  .form-wrapper {
    margin-top: 3rem;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    gap: 4rem;
  }

  .backToTop {
    padding: 0.4rem 1rem;
    background-color: var(--bg);
    text-align: center;
  }

  label {
    display: flex;
    flex-direction: column;
    font-size: 1rem;
    color: grey;
  }

  .footer-wrapper input,
  .footer-wrapper textarea {
    border: 0;
    width: 25rem;
    height: 50px;
    background-color: var(--bg-form);
    border-bottom: 2px solid var(--secondary);
    margin-bottom: 2rem;
  }
  .btn {
    margin-top: 0.75rem;
    margin-left: auto;
  }

  .right-wrapper textarea {
    height: 11rem;
    resize: none;
  }

  .footer-wrapper label {
    margin-bottom: 0.5rem;
  }

  @media screen and (max-width: 900px) {
    .form-wrapper {
      flex-direction: column;
      align-items: center;
    }
    .footer-wrapper input,
    .footer-wrapper textarea {
      width: 90vw;
    }
  }
</style>
