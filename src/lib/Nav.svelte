<script lang="ts">
  // let inactive = true;
  // let mode_dark = false;
  // let root_doc = document.documentElement;
  // let schemes: string;

  // if (localStorage.getItem("mode") == "light") {
  //   mode_dark = true;
  //   root_doc.classList.add("light");
  // }

  // function toggleMode() {
  //   if (mode_dark) {
  //     schemes = "dark";
  //     root_doc.classList.remove("light");
  //   } else {
  //     schemes = "light";
  //     root_doc.classList.add("light");
  //   }
  //   localStorage.setItem("mode", schemes);
  //   mode_dark = !mode_dark;
  // }
</script>

<nav class="nav-wrapper wrapper" id="header">
  <div class="nav-mobile">
    <h1 class='brand'>AFRIAN.</h1>
    <!-- <div class="toggle" on:click={toggleMode}>
      <span class="toggle-button" class:toggle-pos={mode_dark} />
    </div>
    <div class="menu" on:click={() => (inactive = !inactive)}>
      <svg
        class:visible={!inactive}
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        ><path d="M3 4h18v2H3V4Zm6 7h12v2H9v-2Zm-6 7h18v2H3v-2Z" /></svg
      >

      <svg
        class:visible={inactive}
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 256 256"
        ><path
          d="M208.49 191.51a12 12 0 0 1-17 17L128 145l-63.51 63.49a12 12 0 0 1-17-17L111 128L47.51 64.49a12 12 0 0 1 17-17L128 111l63.51-63.52a12 12 0 0 1 17 17L145 128Z"
        /></svg
      >
    </div> -->
  </div>
  <ul class="navbar">
    <li><a href="#projects">PROJECTS</a></li>
    <li><a href="#contact">CONTACT</a></li>
  </ul>
</nav>

<style>

  .nav-wrapper {
    padding: 2rem;
    font-family: var(--font-epi);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .navbar {
    transition: all 0.5s ease-in-out;
    width: 100%;
    display: flex;
    list-style: none;
    justify-content: right;
    align-items: center;
    gap: 25px;
  }
  li a {
    text-decoration: none;
    padding: 0;
    color: var(--text-color);
  }
  .navbar li {
    border: 2px solid transparent;
    cursor: pointer;
  }

  .navbar li:hover {
    border-bottom: 2px solid var(--secondary);
  }

  .toggle {
    position: relative;
    width: 60px;
    height: 25px;
    border-radius: 50px;
    background-color: var(--toggle);
    cursor: pointer;
  }
  .toggle-button {
    transition: all ease 0.5s;
    position: absolute;
    background-color: var(--secondary);
    height: 15px;
    width: 15px;
    top: 5px;
    left: 5px;
    border-radius: 50%;
  }

  .toggle-pos {
    left: 40px;
  }

  .menu {
    display: none;
  }
  .menu svg path {
    fill: var(--secondary);
  }
  .inactive {
    display: none;
  }

  @media screen and (max-width: 1055px) {
    .navbar {
      justify-content: center;
    }
  }
  @media screen and (min-width: 600px) {
    .inactive {
      display: flex;
    }
  }

  @media screen and (max-width: 600px) {
    .nav-mobile {
      display: flex;
      width: 100%;
      justify-content: space-between;
    }
    .nav-wrapper {
      padding: 1rem 2rem;
      border-top: 2px solid var(--secondary);
      flex-direction: column;
      background-color: var(--bg);
      box-shadow: 0px 20px 40px var(--shadow);
    }

    .navbar {
      margin-top: 2rem;
      flex-direction: column;
    }
    .navbar > * {
      margin: 0.75rem 0;
    }
    .menu {
      display: block;
    }
  }
</style>
