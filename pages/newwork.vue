<template>
    <body>
      <header class="header" id="header">
        <nav class="nav container">
          <a href="#" class="nav__logo">Thomas</a>

          <div class="nav__menu" id="nav-menu">
            <ul class="nav__list grid">
              <li class="nav__item">
                <a href="#home" class="nav__link">
                  <i class="uil uil-estate"></i> Home
                </a>
              </li>

              <li class="nav__item">
                <a href="#about" class="nav__link">
                  <i class="uil uil-user"></i> About
                </a>
              </li>

              <li class="nav__item">
                <a href="#skills" class="nav__link">
                  <i class="uil uil-file-alt"></i> Skills
                </a>
              </li>

              <li class="nav__item">
                <a href="#services" class="nav__link">
                  <i class="uil uil-briefcase-alt"></i> Services
                </a>
              </li>

              <li class="nav__item">
                <a href="#portfolio" class="nav__link">
                  <i class="uil uil-scenery"></i> Portfolio
                </a>
              </li>

              <li class="nav__item">
                <a href="#contact" class="nav__link">
                  <i class="uil uil-message"></i> Contactme
                </a>
              </li>
            </ul>

            <i class="uil uil-times nav__close" id="nav-close"></i>
          </div>

          <div class="nav__btns">
            <!-- Theme change button -->
            <i class="uil uil-moon change-theme" id="theme-button"></i>

            <div class="nav__toggle" id="nav-toggle">
              <i class="uil uil-apps"></i>
            </div>
          </div>
        </nav>
      </header>
    </body>
</template>
