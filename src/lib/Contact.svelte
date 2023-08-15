<script lang="ts">
  import Airtable from "airtable";
  import Swal from "sweetalert2";

  let reset_value_name = "";
  let reset_value_email = "";
  let reset_value_desc = "";

  let sendable = true;

  const api_key = import.meta.env.VITE_AIRTABLE_ACCESS;
  const api_base = import.meta.env.VITE_AIRTABLE_BASE;

  function getInquiry(param) {
    if (sendable == false) {
      return;
    }
    sendable = false;

    for (const idx in [0, 1, 2]) {
      if (param.target[idx].value == "") {
        let alert_message = {
          icon: "error",
          title:
            "<p class='fn'>Value Cannot Be Empty. <br>  <small>Please, Try Again!</small></p>",
        };
        alert(alert_message);
        sendable = true;
        return;
      }
    }

    let base = new Airtable({
      apiKey: api_key,
    }).base(api_base);

    base("inquiries").create(
      [
        {
          fields: {
            Names: param.target[0].value,
            Emails: param.target[1].value,
            Messages: param.target[2].value,
          },
        },
      ],
      function status(err) {
        reset();
        sendable = true;

        if (err) {
          console.error(err);

          let alert_message = {
            icon: "error",
            title: "<p class='fn'>Failed to Send Message.</p>",
          };

          alert(alert_message);
          sendable = true;
          return;
        }

        let alert_message = {
          icon: "success",
          title: "<p class='fn'>Message Successfuly Sent</p>",
        };

        alert(alert_message);
      }
    );
  }

  function alert(message) {
    const Toast = Swal.mixin({
      toast: true,
      position: "bottom-end",
      showConfirmButton: false,
      timer: 3000,
      timerProgressBar: true,
      didOpen: (toast) => {
        toast.addEventListener("mouseenter", Swal.stopTimer);
        toast.addEventListener("mouseleave", Swal.resumeTimer);
      },
    });

    Toast.fire({
      icon: message.icon,
      title: message.title,
    });
  }

  function reset() {
    reset_value_name = "";
    reset_value_email = "";
    reset_value_desc = "";
  }
</script>

<section class="main" id="contact">
  <div class="footer-wrapper">
    <div class="contact-wrapper">
      <h1 class="text-header">Contact</h1>
      <a href="#header" class="backToTop"
        ><svg
          class="icon"
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
    <form
      method="post"
      class="form-wrapper"
      on:submit|preventDefault={getInquiry}
    >
      <div class="left-wrapper">
        <label for="name">Name</label>
        <input
          type="text"
          name="name"
          id="name"
          bind:value={reset_value_name}
        />
        <label for="email">Email</label>
        <input
          type="email"
          name="email"
          id="email"
          bind:value={reset_value_email}
        />
      </div>
      <div class="right-wrapper">
        <label for="message">Message</label>
        <textarea
          name="message"
          id="message"
          cols="50"
          rows="50"
          bind:value={reset_value_desc}
        />
        <button
          type="submit"
          class="btn"
          disabled={!sendable}
          class:disable-submit={!sendable}
        >
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
    </form>
  </div>
</section>

<style>
  .disable-submit {
    opacity: 0.3;
    cursor: not-allowed;
    filter: brightness(0.5);
  }
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
    z-index: 1;
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
    text-transform: uppercase;
    grid-area: 1;
  }

  .contact-wrapper {
    display: flex;
    max-width: 55rem;
    margin: auto;
    justify-content: space-between;
  }

  .form-wrapper {
    position: relative;
    z-index: 2;
    margin-top: 3rem;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    font-family: var(--font-epi);
    gap: 4rem;
  }

  .backToTop {
    padding: 0.4rem 1rem;
    background-color: var(--bg);
    text-align: center;
    border: 1px solid transparent;
  }

  .backToTop:hover {
    transition: all 0.5s ease;
    border: 1px solid var(--secondary);
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
    padding: 0.75rem;
    width: 25rem;
    height: 50px;
    background-color: var(--bg-form);
    border-bottom: 2px solid var(--secondary);
    margin-bottom: 2rem;
    color: var(--text-color);
    font-size: 1rem;
    font-weight: 400;
  }
  .btn {
    margin-top: 0.75rem;
    margin-left: auto;
  }

  .btn:hover svg {
    transition: all 0.5s ease;
    transform: translateX(5px);
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
  @media screen and (max-width: 600px) {
    .footer-wrapper {
      padding: 0;
    }
    .contact-wrapper {
      margin: 2rem 1.5rem 0;
    }
  }
</style>
