<script lang="ts">
</script>

<section class="main" id="contact">
  <div class="footer-wrapper">
    <div class="contact-wrapper">
      <h1>Contact</h1>
      <span class="backToTop" />
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
        <textarea name="" id="" cols="30" rows="10">sop</textarea>
        <!-- <button class="btn">
          Kirim
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
        > -->
      </div>
    </div>
  </div>
</section>

<style>
  #contact {
    background-color: var(--tertiery-bg);
    padding: 5rem 0;
    margin-top: 1rem;
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
    margin-top: 5rem;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    gap: 4rem;
  }

  .backToTop {
    width: 60px;
    height: 60px;
    background-color: var(--bg);
  }

  label {
    display: flex;
    flex-direction: column;
    font-size: 1rem;
  }
  .footer-wrapper input,
  .footer-wrapper textarea {
    border: 0;
    width: 25rem;
    height: 50px;
    background-color: var(--bg-form);
    border-bottom: 2px solid var(--secondary);
  }

  .right-wrapper textarea {
    height: 25rem;
    width: 25rem;
  }
</style>
