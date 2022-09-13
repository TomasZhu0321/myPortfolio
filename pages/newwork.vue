<template>
  <body>
    <header class="header" id="header">
      <nav class="nav container">
        <a href="#" class="nav__logo">Thomas</a>
        <div class="nav__menu" id="nav-menu">
          <ul class="nav__list grid">
            <li class="nav__item">
              <a href="#home" class="nav__link">
                <i class="uil uil-estate nav__icon"></i> Home
              </a>
            </li>

            <li class="nav__item">
              <a href="#about" class="nav__link">
                <i class="uil uil-user nav__icon"></i> About
              </a>
            </li>

            <li class="nav__item">
              <a href="#skills" class="nav__link">
                <i class="uil uil-file-alt nav__icon"></i> Skills
              </a>
            </li>

            <li class="nav__item">
              <a href="#services" class="nav__link">
                <i class="uil uil-briefcase-alt nav__icon"></i> Services
              </a>
            </li>

            <li class="nav__item">
              <a href="#portfolio" class="nav__link">
                <i class="uil uil-scenery nav__icon"></i> Portfolio
              </a>
            </li>

            <li class="nav__item">
              <a href="#contact" class="nav__link">
                <i class="uil uil-message nav__icon"></i> Contactme
              </a>
            </li>
          </ul>

          <i class="uil uil-times nav__close" id="nav-close"></i>
        </div>

        <div class="nav__btns">
          <div class="nav__toggle" id="nav-toggle">
            <i class="uil uil-apps"></i>
          </div>
        </div>
      </nav>
    </header>
  </body>
</template>

<script>
export default {
  mounted() {
    /*==================== MENU SHOW Y HIDDEN ====================*/
    const navMenu = document.getElementById("nav-menu"),
      navToggle = document.getElementById("nav-toggle"),
      navClose = document.getElementById("nav-close");

    /*===== MENU SHOW =====*/
    /* Validate if constant exists */
    if (navToggle) {
      navToggle.addEventListener("click", () => {
        navMenu.classList.add("show-menu");
      });
    }

    /*===== MENU HIDDEN =====*/
    /* Validate if constant exists */
    if (navClose) {
      navClose.addEventListener("click", () => {
        navMenu.classList.remove("show-menu");
      });
    }

    /*==================== REMOVE MENU MOBILE ====================*/
    const navLink = document.querySelectorAll(".nav__link");

    function linkAction() {
      const navMenu = document.getElementById("nav-menu");
      // When we click on each nav__link, we remove the show-menu class
      navMenu.classList.remove("show-menu");
    }
    navLink.forEach((n) => n.addEventListener("click", linkAction));
  },
};
</script>
