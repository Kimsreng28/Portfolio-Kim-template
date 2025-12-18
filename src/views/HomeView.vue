<template>
  <div id="app" :class="modeClasses">
    <!-- Navigation -->
    <nav
      class="fixed top-0 w-full z-50 py-4 sm:py-5 px-4 sm:px-6 shadow-xl border-b transition-all duration-300"
      :class="navClasses"
      :style="{ transform: navTransform }"
    >
      <div class="container mx-auto flex justify-between items-center">
        <!-- Logo with icon - Improved for mobile & tablet -->
        <div class="flex items-center space-x-2 sm:space-x-3">
          <div
            class="w-9 h-9 sm:w-10 sm:h-10 md:w-12 md:h-12 rounded-lg flex items-center justify-center shadow-lg transition-colors duration-300 flex-shrink-0"
            :class="logoClasses"
          >
            <svg
              class="w-5 h-5 sm:w-6 sm:h-6 md:w-7 md:h-7"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"
              />
            </svg>
          </div>
          <div class="text-lg sm:text-xl md:text-2xl font-bold flex items-center gap-1 sm:gap-2">
            <span :class="logoTextClasses" class="leading-tight">HAI</span>
            <span :class="textColor" class="leading-tight">KIMSRENG</span>
          </div>
        </div>

        <!-- Desktop Navigation with Icons - Tablet optimized -->
        <div
          class="hidden md:flex items-center space-x-0 lg:space-x-1 backdrop-blur-sm px-2 lg:px-3 py-1.5 lg:py-2 rounded-full border transition-all duration-300"
          :class="navContainerClasses"
        >
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="'#' + item.id"
            @click.prevent="scrollTo(item.id)"
            class="nav-link group relative px-2 lg:px-4 py-1.5 lg:py-2 rounded-full transition-all duration-300 flex items-center space-x-1 lg:space-x-2"
            :class="navLinkClasses"
          >
            <!-- Icon - Always visible on tablet/desktop -->
            <span :class="navIconClasses">
              <svg
                class="w-3.5 h-3.5 lg:w-4 lg:h-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  v-if="item.icon"
                  :d="item.icon"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                />
              </svg>
            </span>
            <!-- Text - Hide on tablet, show on desktop -->
            <span :class="navTextClasses" class="hidden lg:inline">
              {{ item.name }}
            </span>
            <!-- Active indicator -->
            <span
              class="absolute bottom-0 left-1/2 transform -translate-x-1/2 w-0 group-hover:w-6 lg:group-hover:w-8 h-0.5 rounded-full transition-all duration-300"
              :class="navIndicatorClasses"
            ></span>
          </a>
        </div>

        <!-- Right side - Theme Toggle & Mobile Menu -->
        <div class="flex items-center space-x-3 sm:space-x-4">
          <!-- Theme Toggle Button -->
          <button
            @click="toggleTheme"
            class="relative w-10 h-10 sm:w-11 sm:h-11 md:w-12 md:h-12 rounded-full flex items-center justify-center transition-all duration-300 shadow-lg border flex-shrink-0"
            :class="themeToggleClasses"
            aria-label="Toggle theme"
          >
            <div class="relative w-5 h-5 sm:w-5 sm:h-5 md:w-6 md:h-6">
              <!-- Sun Icon -->
              <svg
                v-if="darkMode"
                class="w-4 h-4 sm:w-4 sm:h-4 md:w-5 md:h-5 absolute inset-0 m-auto text-yellow-300 transition-all duration-300 opacity-100"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
                  clip-rule="evenodd"
                />
              </svg>
              <!-- Moon Icon -->
              <svg
                v-else
                class="w-4 h-4 sm:w-4 sm:h-4 md:w-5 md:h-5 absolute inset-0 m-auto text-gray-700 transition-all duration-300 opacity-100"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
              </svg>
            </div>
          </button>

          <!-- Mobile Menu Button - Hide on tablet/desktop -->
          <div class="md:hidden">
            <button
              @click="mobileMenuOpen = !mobileMenuOpen"
              class="relative w-10 h-10 sm:w-11 sm:h-11 rounded-full flex items-center justify-center transition-all duration-300 shadow-lg border flex-shrink-0"
              :class="mobileMenuButtonClasses"
              aria-label="Toggle menu"
            >
              <div class="relative w-5 h-5 sm:w-5 sm:h-5">
                <span
                  :class="[
                    'absolute top-1 left-0 w-5 sm:w-5 h-0.5 rounded-full transition-all duration-300',
                    mobileMenuLineClasses,
                    { 'top-2 rotate-45': mobileMenuOpen, 'top-1': !mobileMenuOpen },
                  ]"
                ></span>
                <span
                  :class="[
                    'absolute top-2 left-0 w-5 sm:w-5 h-0.5 rounded-full transition-all duration-300',
                    mobileMenuLineClasses,
                    { 'opacity-0': mobileMenuOpen },
                  ]"
                ></span>
                <span
                  :class="[
                    'absolute bottom-1 left-0 w-5 sm:w-5 h-0.5 rounded-full transition-all duration-300',
                    mobileMenuLineClasses,
                    {
                      'bottom-2 -rotate-45': mobileMenuOpen,
                      'bottom-1': !mobileMenuOpen,
                    },
                  ]"
                ></span>
              </div>
            </button>
          </div>
        </div>
      </div>

      <!-- Mobile Menu with Icons - Tablet optimized -->
      <div
        v-if="mobileMenuOpen"
        class="md:hidden backdrop-blur-lg mt-4 py-4 px-4 sm:px-6 rounded-2xl shadow-2xl border mx-3 sm:mx-4 transition-all duration-300"
        :class="mobileMenuClasses"
      >
        <div class="flex flex-col space-y-2">
          <a
            v-for="(item, index) in navItems"
            :key="item.id"
            :href="'#' + item.id"
            @click.prevent="scrollToAndCloseMenu(item.id)"
            class="mobile-nav-link group relative px-4 sm:px-5 py-3 rounded-xl transition-all duration-300 flex items-center space-x-3"
            :class="mobileNavLinkClasses"
            :style="{ '--i': index }"
          >
            <!-- Icon container -->
            <div
              class="w-9 h-9 sm:w-10 sm:h-10 rounded-lg flex items-center justify-center transition-all duration-300 flex-shrink-0"
              :class="mobileNavIconContainerClasses"
            >
              <span :class="mobileNavIconClasses">
                <svg
                  class="w-4 h-4 sm:w-5 sm:h-5"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    v-if="item.icon"
                    :d="item.icon"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                  />
                </svg>
              </span>
            </div>
            <!-- Text -->
            <div class="flex-1 min-w-0">
              <span class="text-sm sm:text-base font-medium truncate" :class="mobileNavTextClasses">
                {{ item.name }}
              </span>
            </div>
            <!-- Arrow indicator -->
            <span :class="mobileNavArrowClasses" class="flex-shrink-0">
              <svg
                class="w-4 h-4 sm:w-5 sm:h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 5l7 7-7 7"
                />
              </svg>
            </span>
          </a>
        </div>

        <!-- Mobile Menu Footer -->
        <div class="mt-6 pt-4 border-t" :class="mobileMenuFooterClasses">
          <div class="flex items-center justify-center space-x-4">
            <a
              href="https://github.com/Kimsreng28"
              target="_blank"
              class="p-2 rounded-lg transition-all duration-300"
              :class="socialIconClasses"
              aria-label="GitHub"
            >
              <svg
                class="w-5 h-5 transition-colors duration-300"
                :class="socialIconSvgClasses"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                />
              </svg>
            </a>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex items-center pt-16 relative overflow-hidden">
      <!-- Background Effects -->
      <div class="absolute inset-0 z-0">
        <div
          class="absolute top-1/4 left-1/4 w-64 h-64 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-pulse"
          :class="heroBgCircle1"
        ></div>
        <div
          class="absolute bottom-1/4 right-1/4 w-96 h-96 rounded-full mix-blend-multiply filter blur-3xl opacity-10 animate-pulse delay-1000"
          :class="heroBgCircle2"
        ></div>
        <div
          class="absolute top-3/4 left-1/2 w-80 h-80 rounded-full mix-blend-multiply filter blur-3xl opacity-15 animate-pulse delay-500"
          :class="heroBgCircle3"
        ></div>
      </div>

      <div class="container mx-auto px-4 sm:px-6 py-12 md:py-20 relative z-10">
        <div class="flex flex-col lg:flex-row items-center justify-between gap-8 lg:gap-12">
          <!-- Left Content -->
          <div ref="leftContent" class="lg:w-1/2 w-full">
            <div class="mb-6 md:mb-8">
              <div
                class="inline-block px-4 py-2 rounded-full mb-4 md:mb-6 transition-colors duration-300"
                :class="heroBadgeClasses"
              >
                <span :class="heroBadgeTextClasses">🚀 FULL-STACK DEVELOPER</span>
              </div>
              <h1
                class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold mb-3 md:mb-4 leading-tight"
              >
                <span :class="heroTitleClasses"> HAI KIMSRENG </span>
              </h1>
              <h2 class="text-xl sm:text-2xl md:text-3xl mb-4 md:mb-6" :class="heroSubtitleClasses">
                <span :class="heroSubtitleSpan1">Software Engineer</span> &
                <span :class="heroSubtitleSpan2">Mobile Developer</span>
              </h2>
              <p
                class="text-base sm:text-lg md:text-lg mb-6 md:mb-8 max-w-2xl"
                :class="heroTextClasses"
              >
                Crafting digital experiences with cutting-edge technologies. Specialized in building
                scalable web applications, real-time systems, and cross-platform mobile solutions
                that solve real-world problems.
              </p>
            </div>

            <!-- Quick Stats -->
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-3 md:gap-4 mb-6 md:mb-8">
              <div
                v-for="stat in quickStats"
                :key="stat.label"
                class="backdrop-blur-sm p-3 sm:p-4 rounded-xl border transition-colors duration-300"
                :class="quickStatsClasses"
              >
                <div :class="quickStatsNumberClasses">{{ stat.number }}</div>
                <div class="text-xs sm:text-sm" :class="quickStatsLabelClasses">
                  {{ stat.label }}
                </div>
              </div>
            </div>

            <!-- Tech Stack -->
            <div class="mb-6 md:mb-8">
              <h3
                class="text-base sm:text-lg font-semibold mb-3 md:mb-4"
                :class="techStackTitleClasses"
              >
                Tech Stack
              </h3>
              <div class="flex flex-wrap gap-2 md:gap-3">
                <div
                  v-for="tech in mainTech"
                  :key="tech"
                  class="px-3 sm:px-4 py-1.5 sm:py-2 rounded-lg border transition-all duration-300 group cursor-pointer"
                  :class="techStackItemClasses"
                >
                  <span :class="techStackTextClasses">
                    {{ tech }}
                  </span>
                </div>
              </div>
            </div>

            <!-- CTA Buttons -->
            <div class="flex flex-col sm:flex-row flex-wrap gap-3 sm:gap-4 w-full">
              <!-- Primary Button - Get In Touch -->
              <button
                @click="scrollTo('contact')"
                class="px-4 sm:px-6 py-3.5 sm:py-3 rounded-lg font-semibold transition-all duration-300 flex items-center justify-center shadow-lg hover:shadow-xl w-full sm:w-auto sm:flex-1 min-h-[50px] sm:min-h-0"
                :class="ctaButtonPrimaryClasses"
              >
                <svg
                  class="w-5 h-5 sm:w-4 sm:h-4 mr-2.5 sm:mr-2 flex-shrink-0"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                  />
                </svg>
                <span class="text-sm sm:text-base whitespace-nowrap">Get In Touch</span>
              </button>

              <!-- Secondary Button - View GitHub -->
              <a
                href="https://github.com/Kimsreng28"
                target="_blank"
                class="px-4 sm:px-6 py-3.5 sm:py-3 rounded-lg font-semibold transition-all duration-300 flex items-center justify-center border w-full sm:w-auto sm:flex-1 min-h-[50px] sm:min-h-0"
                :class="ctaButtonSecondaryClasses"
              >
                <svg
                  class="w-5 h-5 sm:w-4 sm:h-4 mr-2.5 sm:mr-2 flex-shrink-0"
                  fill="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                  />
                </svg>
                <span class="text-sm sm:text-base whitespace-nowrap">View GitHub</span>
              </a>

              <!-- Tertiary Button - View Projects -->
              <button
                @click="scrollTo('projects')"
                class="px-4 sm:px-6 py-3.5 sm:py-3 rounded-lg font-semibold transition-all duration-300 flex items-center justify-center border w-full sm:w-auto sm:flex-1 min-h-[50px] sm:min-h-0"
                :class="ctaButtonTertiaryClasses"
              >
                <svg
                  class="w-5 h-5 sm:w-4 sm:h-4 mr-2.5 sm:mr-2 flex-shrink-0"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"
                  />
                </svg>
                <span class="text-sm sm:text-base whitespace-nowrap">View Projects</span>
              </button>
            </div>
          </div>

          <!-- Right Content - Profile Image & Info -->
          <div ref="rightContent" class="lg:w-1/2 flex justify-center mt-8 lg:mt-0">
            <div class="relative w-full max-w-sm lg:max-w-md">
              <!-- Main Profile Card -->
              <div class="relative z-20">
                <!-- Profile Image Container -->
                <div
                  class="relative w-48 h-48 sm:w-64 sm:h-64 md:w-80 md:h-80 lg:w-96 lg:h-96 mx-auto"
                >
                  <!-- Stars - Responsive positioning -->
                  <div class="absolute inset-0 z-15">
                    <!-- Star 1 - Top Right -->
                    <div
                      class="absolute star-decoration"
                      :class="{
                        'top-10 -right-2 sm:top-10 sm:right-2 md:top-12 md:right-0 lg:top-10 lg:right-2': true,
                      }"
                      style="animation-delay: 0s"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 lg:w-7 lg:h-7"
                        :class="darkMode ? 'text-blue-400' : 'text-blue-500'"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z"
                        />
                      </svg>
                    </div>

                    <!-- Star 2 - Top Left -->
                    <div
                      class="absolute star-decoration"
                      :class="{
                        'top-2 left-4 sm:top-3 sm:left-10 md:top-4 md:left-8 lg:top-2 lg:left-12': true,
                      }"
                      style="animation-delay: 0.8s"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 lg:w-7 lg:h-7"
                        :class="darkMode ? 'text-blue-400' : 'text-blue-500'"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z"
                        />
                      </svg>
                    </div>

                    <!-- Star 3 - Bottom Left -->
                    <div
                      class="absolute star-decoration"
                      :class="{
                        'bottom-8 -left-2 sm:bottom-10 sm:left-3 md:bottom-8 md:left-2 lg:bottom-10 lg:left-2': true,
                      }"
                      style="animation-delay: 1.6s"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 lg:w-7 lg:h-7"
                        :class="darkMode ? 'text-blue-400' : 'text-blue-500'"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z"
                        />
                      </svg>
                    </div>

                    <!-- Star 4 - Bottom Right -->
                    <div
                      class="absolute star-decoration"
                      :class="{
                        'bottom-4 -right-0 sm:bottom-3 sm:right-10 md:bottom-2 md:right-10 lg:bottom-3 lg:right-10': true,
                      }"
                      style="animation-delay: 2.4s"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 lg:w-7 lg:h-7"
                        :class="darkMode ? 'text-blue-400' : 'text-blue-500'"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z"
                        />
                      </svg>
                    </div>
                  </div>

                  <!-- Khmer Cultural Flower Border - Responsive positioning -->
                  <div class="absolute inset-0 z-20">
                    <!-- Top Left Flower -->
                    <div
                      class="absolute khmer-flower"
                      :class="{
                        '-top-4 -left-6 sm:-top-5 sm:-left-5 md:-top-6 md:-left-6 lg:-top-7 lg:-left-7': true,
                      }"
                      style="--rotation: -12deg"
                    >
                      <img
                        src="../assets/images/flower.png"
                        alt="Khmer Flower"
                        class="w-10 h-10 sm:w-12 sm:h-12 md:w-14 md:h-14 lg:w-16 lg:h-16 object-contain filter brightness-75 drop-shadow-lg"
                      />
                    </div>

                    <!-- Top Right Flower -->
                    <div
                      class="absolute khmer-flower"
                      :class="{
                        '-top-0 -right-2 sm:-top-5 sm:-right-5 md:-top-4 md:-right-4 lg:-top-7 lg:-right-7': true,
                      }"
                      style="--rotation: 12deg; animation-delay: 0.5s"
                    >
                      <img
                        src="../assets/images/flower.png"
                        alt="Khmer Flower"
                        class="w-10 h-10 sm:w-12 sm:h-12 md:w-14 md:h-14 lg:w-16 lg:h-16 object-contain filter brightness-75 drop-shadow-lg"
                      />
                    </div>

                    <!-- Bottom Left Flower -->
                    <div
                      class="absolute khmer-flower"
                      :class="{
                        '-bottom-2 -left-4 sm:-bottom-5 sm:-left-5 md:-bottom-4 md:-left-10 lg:-bottom-7 lg:-left-7': true,
                      }"
                      style="--rotation: 12deg; animation-delay: 1s"
                    >
                      <img
                        src="../assets/images/flower.png"
                        alt="Khmer Flower"
                        class="w-10 h-10 sm:w-12 sm:h-12 md:w-14 md:h-14 lg:w-16 lg:h-16 object-contain filter brightness-75 drop-shadow-lg"
                      />
                    </div>

                    <!-- Bottom Right Flower -->
                    <div
                      class="absolute khmer-flower"
                      :class="{
                        '-bottom-6 -right-4 sm:-bottom-5 sm:-right-5 md:-bottom-6 md:-right-6 lg:-bottom-7 lg:-right-7': true,
                      }"
                      style="--rotation: -12deg; animation-delay: 1.5s"
                    >
                      <img
                        src="../assets/images/flower.png"
                        alt="Khmer Flower"
                        class="w-10 h-10 sm:w-12 sm:h-12 md:w-14 md:h-14 lg:w-16 lg:h-16 object-contain filter brightness-75 drop-shadow-lg"
                      />
                    </div>
                  </div>

                  <!-- Traditional Pattern Border with Animation -->
                  <div
                    class="absolute inset-0 rounded-full border-2 sm:border-3 md:border-4 z-10 khmer-border"
                    :class="darkMode ? 'border-gray-600/20' : 'border-gray-400/20'"
                    style="
                      background-image: repeating-conic-gradient(
                        from 0deg,
                        transparent 0deg 10deg,
                        rgba(100, 100, 100, 0.05) 10deg 20deg
                      );
                    "
                  ></div>

                  <!-- Outer Glow Ring -->
                  <div
                    class="absolute inset-0 rounded-full animate-spin-slow z-0"
                    :class="profileRingClasses"
                    style="animation-duration: 8s"
                  ></div>

                  <!-- Profile Image Background with Subtle Pattern -->
                  <div
                    class="absolute inset-2 sm:inset-3 md:inset-4 rounded-full flex items-center justify-center overflow-hidden z-10"
                    :class="profileBgClasses"
                  >
                    <!-- Decorative pattern overlay -->
                    <div class="absolute inset-0 opacity-5">
                      <div
                        class="absolute top-0 left-0 w-full h-full"
                        style="
                          background-image:
                            radial-gradient(
                              circle at 25% 25%,
                              rgba(150, 150, 150, 0.1) 0%,
                              transparent 50%
                            ),
                            radial-gradient(
                              circle at 75% 75%,
                              rgba(150, 150, 150, 0.1) 0%,
                              transparent 50%
                            );
                        "
                      ></div>
                    </div>

                    <!-- Profile Image Placeholder -->
                    <div
                      class="relative w-full h-full rounded-full overflow-hidden border sm:border-2"
                      :class="darkMode ? 'border-gray-700/20' : 'border-gray-600/20'"
                    >
                      <!-- Fallback Initials with decoration -->
                      <div
                        v-if="!profileImageLoaded"
                        class="w-full h-full flex items-center justify-center relative"
                        :class="profileFallbackClasses"
                      >
                        <!-- Decorative corner elements with animation -->
                        <div
                          class="absolute top-1 left-1 sm:top-2 sm:left-2 md:top-3 md:left-3 border-t border-l corner-decoration"
                          :class="[
                            darkMode ? 'border-gray-500' : 'border-gray-600',
                            'w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6',
                          ]"
                        ></div>
                        <div
                          class="absolute top-1 right-1 sm:top-2 sm:right-2 md:top-3 md:right-3 border-t border-r corner-decoration"
                          :class="[
                            darkMode ? 'border-gray-500' : 'border-gray-600',
                            'w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6',
                          ]"
                          style="animation-delay: 0.2s"
                        ></div>
                        <div
                          class="absolute bottom-1 left-1 sm:bottom-2 sm:left-2 md:bottom-3 md:left-3 border-b border-l corner-decoration"
                          :class="[
                            darkMode ? 'border-gray-500' : 'border-gray-600',
                            'w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6',
                          ]"
                          style="animation-delay: 0.4s"
                        ></div>
                        <div
                          class="absolute bottom-1 right-1 sm:bottom-2 sm:right-2 md:bottom-3 md:right-3 border-b border-r corner-decoration"
                          :class="[
                            darkMode ? 'border-gray-500' : 'border-gray-600',
                            'w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6',
                          ]"
                          style="animation-delay: 0.6s"
                        ></div>

                        <div class="text-center relative z-10 px-2">
                          <div
                            class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl font-bold leading-none"
                            :class="profileInitialsClasses"
                          >
                            HK
                          </div>
                          <div
                            class="mt-1 sm:mt-2 md:mt-3 lg:mt-4 text-sm sm:text-base md:text-lg lg:text-xl"
                            :class="profileTitleClasses"
                          >
                            Developer
                          </div>
                        </div>
                      </div>

                      <!-- Actual Profile Image with overlay -->
                      <div v-else class="relative w-full h-full">
                        <img
                          src="../assets/images/Kimsreng.jpg"
                          alt="Profile Kim"
                          class="w-full h-full object-cover"
                        />
                        <!-- Subtle pattern overlay on image -->
                        <div
                          class="absolute inset-0 mix-blend-overlay opacity-3"
                          style="
                            background-image: repeating-linear-gradient(
                              45deg,
                              transparent,
                              transparent 10px,
                              rgba(150, 150, 150, 0.1) 10px,
                              rgba(150, 150, 150, 0.1) 20px
                            );
                          "
                        ></div>
                      </div>
                    </div>
                  </div>

                  <!-- Floating Tech Badges - Responsive positioning -->
                  <div
                    class="absolute badge-float"
                    :class="[
                      'text-white rounded-lg shadow-lg transform rotate-6 z-30 border',
                      'px-2 py-1 text-xs -top-6 -right-6',
                      'sm:px-3 sm:py-1.5 sm:text-sm sm:-top-7 sm:-right-7',
                      'md:px-3 md:py-1.5 md:text-sm md:-top-8 md:-right-8',
                      'lg:px-4 lg:py-2 lg:text-sm lg:-top-9 lg:-right-9',
                      floatingBadgeClasses,
                      darkMode ? 'border-gray-600' : 'border-gray-500',
                    ]"
                    style="animation-delay: 0s"
                  >
                    <div class="font-bold flex items-center">
                      <div
                        class="w-1.5 h-1.5 sm:w-2 sm:h-2 rounded-full mr-1 sm:mr-2 badge-dot"
                        :class="darkMode ? 'bg-gray-300' : 'bg-gray-600'"
                      ></div>
                      Laravel
                    </div>
                  </div>

                  <div
                    class="absolute badge-float"
                    :class="[
                      'text-white rounded-lg shadow-lg transform -rotate-6 z-30 border',
                      'px-2 py-1 text-xs -bottom-6 -left-6',
                      'sm:px-3 sm:py-1.5 sm:text-sm sm:-bottom-7 sm:-left-7',
                      'md:px-3 md:py-1.5 md:text-sm md:-bottom-8 md:-left-8',
                      'lg:px-4 lg:py-2 lg:text-sm lg:-bottom-9 lg:-left-9',
                      floatingBadgeClasses,
                      darkMode ? 'border-gray-600' : 'border-gray-500',
                    ]"
                    style="animation-delay: 0.3s"
                  >
                    <div class="font-bold flex items-center">
                      <div
                        class="w-1.5 h-1.5 sm:w-2 sm:h-2 rounded-full mr-1 sm:mr-2 badge-dot"
                        :class="darkMode ? 'bg-gray-300' : 'bg-gray-600'"
                      ></div>
                      Flutter
                    </div>
                  </div>

                  <div
                    class="absolute badge-float"
                    :class="[
                      'text-white rounded-lg shadow-lg z-30 border',
                      'px-2 py-1 text-xs top-1/2 -right-8',
                      'sm:px-3 sm:py-1.5 sm:text-sm sm:top-1/2 sm:-right-9',
                      'md:px-3 md:py-1.5 md:text-sm md:top-1/2 md:-right-10',
                      'lg:px-4 lg:py-2 lg:text-sm lg:top-1/2 lg:-right-12',
                      floatingBadgeClasses,
                      darkMode ? 'border-gray-600' : 'border-gray-500',
                    ]"
                    style="animation-delay: 0.6s"
                  >
                    <div class="font-bold flex items-center">
                      <div
                        class="w-1.5 h-1.5 sm:w-2 sm:h-2 rounded-full mr-1 sm:mr-2 badge-dot"
                        :class="darkMode ? 'bg-gray-300' : 'bg-gray-600'"
                      ></div>
                      Next.js
                    </div>
                  </div>

                  <div
                    class="absolute badge-float"
                    :class="[
                      'text-white rounded-lg shadow-lg z-30 border',
                      'px-2 py-1 text-xs top-1/2 -left-8',
                      'sm:px-3 sm:py-1.5 sm:text-sm sm:top-1/2 sm:-left-9',
                      'md:px-3 md:py-1.5 md:text-sm md:top-1/2 md:-left-10',
                      'lg:px-4 lg:py-2 lg:text-sm lg:top-1/2 lg:-left-12',
                      floatingBadgeClasses,
                      darkMode ? 'border-gray-600' : 'border-gray-500',
                    ]"
                    style="animation-delay: 0.9s"
                  >
                    <div class="font-bold flex items-center">
                      <div
                        class="w-1.5 h-1.5 sm:w-2 sm:h-2 rounded-full mr-1 sm:mr-2 badge-dot"
                        :class="darkMode ? 'bg-gray-300' : 'bg-gray-600'"
                      ></div>
                      Vue.js
                    </div>
                  </div>

                  <!-- Additional decorative elements with animation -->
                  <div
                    class="absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-2 sm:-translate-y-3 md:-translate-y-4 z-20"
                  >
                    <div
                      class="w-6 h-0.5 sm:w-7 sm:h-0.5 md:w-8 md:h-1 rounded-full pulse-element"
                      :class="darkMode ? 'bg-gray-500' : 'bg-gray-400'"
                    ></div>
                  </div>
                  <div
                    class="absolute bottom-0 left-1/2 transform -translate-x-1/2 translate-y-2 sm:translate-y-3 md:translate-y-4 z-20"
                  >
                    <div
                      class="w-6 h-0.5 sm:w-7 sm:h-0.5 md:w-8 md:h-1 rounded-full pulse-element"
                      :class="darkMode ? 'bg-gray-500' : 'bg-gray-400'"
                      style="animation-delay: 0.5s"
                    ></div>
                  </div>
                </div>

                <!-- Info Card Below Image -->
                <div
                  class="mt-8 sm:mt-8 backdrop-blur-sm rounded-2xl p-4 sm:p-6 border shadow-2xl max-w-sm sm:max-w-md mx-auto"
                  :class="infoCardClasses"
                >
                  <div class="flex items-center justify-between mb-3 sm:mb-4">
                    <div>
                      <h3 class="text-lg sm:text-xl font-bold" :class="infoCardTitleClasses">
                        HAI KIMSRENG
                      </h3>
                      <p :class="infoCardSubtitleClasses">Software Engineer</p>
                    </div>
                    <div
                      class="w-10 h-10 sm:w-12 sm:h-12 rounded-full flex items-center justify-center transition-colors duration-300"
                      :class="infoCardIconClasses"
                    >
                      <svg
                        class="w-5 h-5 sm:w-6 sm:h-6 text-white"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"
                        />
                      </svg>
                    </div>
                  </div>

                  <div class="space-y-2 sm:space-y-3">
                    <div class="flex items-center" :class="infoCardTextClasses">
                      <svg
                        class="w-4 h-4 sm:w-5 sm:h-5 mr-2 sm:mr-3"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                        />
                      </svg>
                      <span>Full-Stack & Mobile Developer</span>
                    </div>
                    <div class="flex items-center" :class="infoCardTextClasses">
                      <svg
                        class="w-4 h-4 sm:w-5 sm:h-5 mr-2 sm:mr-3"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                        />
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                        />
                      </svg>
                      <span>Phnom Penh, Cambodia</span>
                    </div>
                    <div class="flex items-center" :class="infoCardTextClasses">
                      <svg
                        class="w-4 h-4 sm:w-5 sm:h-5 mr-2 sm:mr-3"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
                        />
                      </svg>
                      <span>Available for opportunities</span>
                    </div>
                  </div>

                  <div class="mt-4 sm:mt-6 pt-3 sm:pt-6 border-t" :class="infoCardBorderClasses">
                    <div class="flex justify-center space-x-3 sm:space-x-4">
                      <button @click="scrollTo('contact')" :class="infoCardLinkClasses">
                        Contact Me
                      </button>
                      <span :class="infoCardDividerClasses">•</span>
                      <button @click="scrollTo('projects')" :class="infoCardLinkClasses">
                        View Work
                      </button>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Background Decorative Elements -->
              <div
                class="absolute -top-4 sm:-top-8 -right-4 sm:-right-8 w-20 h-20 sm:w-40 sm:h-40 rounded-full blur-3xl opacity-20 z-0"
                :class="profileDeco1"
              ></div>
              <div
                class="absolute -bottom-4 sm:-bottom-8 -left-4 sm:-left-8 w-24 h-24 sm:w-60 sm:h-60 rounded-full blur-3xl opacity-15 z-0"
                :class="profileDeco2"
              ></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Scroll Indicator -->
      <div
        ref="scrollIndicator"
        class="absolute left-1/2 transform -translate-x-1/2"
        style="bottom: 0"
      >
        <!-- Spacer above the button -->
        <div class="h-8 sm:h-12 w-full"></div>

        <button
          @click="scrollTo('about')"
          class="flex flex-col items-center transition-all duration-300 hover:translate-y-1"
          :class="scrollIndicatorClasses"
        >
          <span class="text-xs sm:text-sm mb-1.5 sm:mb-2 font-medium">Explore More</span>
          <svg
            class="w-5 h-5 sm:w-6 sm:h-6 animate-bounce"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 14l-7 7m0 0l-7-7m7 7V3"
            />
          </svg>
        </button>
      </div>
    </section>

    <!-- Technology Slider Section -->
    <section class="py-8 sm:py-12 overflow-hidden" :class="techSliderClasses">
      <div class="container mx-auto px-4">
        <!-- Section Header -->
        <div class="text-center mb-6 sm:mb-8">
          <div class="inline-flex items-center justify-center mb-3 sm:mb-4">
            <!-- Icon Container -->
            <div
              class="w-8 h-8 sm:w-10 sm:h-10 rounded-full flex items-center justify-center mr-2 sm:mr-3 transition-colors duration-300"
              :class="sectionIconClasses"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                class="w-4 h-4 sm:w-6 sm:h-6 text-white"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M8.25 3v1.5M4.5 8.25H3m18 0h-1.5M4.5 12H3m18 0h-1.5m-15 3.75H3m18 0h-1.5M8.25 19.5V21M12 3v1.5m0 15V21m3.75-18v1.5m0 15V21m-9-1.5h10.5a2.25 2.25 0 0 0 2.25-2.25V6.75a2.25 2.25 0 0 0-2.25-2.25H6.75A2.25 2.25 0 0 0 4.5 6.75v10.5a2.25 2.25 0 0 0 2.25 2.25Zm.75-12h9v9h-9v-9Z"
                />
              </svg>
            </div>
            <h2 class="text-2xl sm:text-3xl font-bold" :class="sectionTitleClasses">
              Technology Stack
            </h2>
          </div>
          <p :class="sectionSubtitleClasses">Technologies I worked with</p>
        </div>

        <!-- Infinite Scroll Container -->
        <div class="relative">
          <!-- Gradient Overlays -->
          <div
            class="absolute left-0 top-0 bottom-0 w-16 sm:w-32 z-10 pointer-events-none"
            :class="techSliderGradientLeft"
          ></div>
          <div
            class="absolute right-0 top-0 bottom-0 w-16 sm:w-32 z-10 pointer-events-none"
            :class="techSliderGradientRight"
          ></div>

          <!-- First Scroll Track -->
          <div class="flex overflow-hidden">
            <div class="flex animate-infinite-scroll py-4">
              <div
                v-for="(tech, index) in techStack"
                :key="'first-' + index"
                class="mx-2 sm:mx-3 md:mx-4 group cursor-pointer"
              >
                <div class="flex flex-col items-center">
                  <!-- Tech Icon/Logo Container -->
                  <div
                    class="w-12 h-12 sm:w-16 sm:h-16 md:w-20 md:h-20 rounded-2xl p-2 sm:p-3 md:p-4 flex items-center justify-center border transition-all duration-300 shadow-lg group-hover:scale-105"
                    :class="techCardClasses"
                  >
                    <!-- Logo Image -->
                    <div v-if="tech.logo" class="relative w-full h-full">
                      <img
                        :src="tech.logo"
                        :alt="tech.name"
                        class="w-full h-full object-contain filter group-hover:brightness-125 transition-all duration-300"
                      />
                    </div>
                  </div>

                  <!-- Tech Name and Category -->
                  <div class="mt-2 sm:mt-3 text-center">
                    <div
                      class="font-semibold transition-colors text-xs sm:text-sm md:text-base"
                      :class="techNameClasses"
                    >
                      {{ tech.name }}
                    </div>
                    <div class="text-xs text-gray-400 mt-1">
                      {{ tech.category }}
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Duplicate for seamless loop -->
            <div class="flex animate-infinite-scroll py-4" aria-hidden="true">
              <div
                v-for="(tech, index) in techStack"
                :key="'second-' + index"
                class="mx-2 sm:mx-3 md:mx-4 group cursor-pointer"
              >
                <div class="flex flex-col items-center">
                  <div
                    class="w-12 h-12 sm:w-16 sm:h-16 md:w-20 md:h-20 rounded-2xl p-2 sm:p-3 md:p-4 flex items-center justify-center border transition-all duration-300 shadow-lg group-hover:scale-105"
                    :class="techCardClasses"
                  >
                    <div v-if="tech.logo" class="relative w-full h-full">
                      <img
                        :src="tech.logo"
                        :alt="tech.name"
                        class="w-full h-full object-contain filter group-hover:brightness-125 transition-all duration-300"
                      />
                    </div>
                  </div>

                  <div class="mt-2 sm:mt-3 text-center">
                    <div
                      class="font-semibold transition-colors text-xs sm:text-sm md:text-base"
                      :class="techNameClasses"
                    >
                      {{ tech.name }}
                    </div>
                    <div class="text-xs text-gray-400 mt-1">
                      {{ tech.category }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-12 sm:py-16 md:py-20" :class="aboutSectionClasses">
      <div class="container mx-auto px-4 sm:px-6">
        <!-- Title with Icon and Underline -->
        <div class="mb-8 sm:mb-12 text-center opacity-0" ref="aboutTitle">
          <div class="inline-flex items-center justify-center mb-3 sm:mb-4">
            <div
              class="w-8 h-8 sm:w-10 sm:h-10 rounded-full flex items-center justify-center mr-2 sm:mr-3 transition-colors duration-300"
              :class="sectionIconClasses"
            >
              <svg
                class="w-4 h-4 sm:w-5 sm:h-5 text-white"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                />
              </svg>
            </div>
            <h2 class="text-2xl sm:text-3xl font-bold" :class="sectionTitleClasses">About Me</h2>
          </div>
          <div class="relative">
            <div
              class="w-16 sm:w-24 h-1 mx-auto rounded-full transition-colors duration-300"
              :class="sectionUnderlineClasses"
            ></div>
            <div
              class="absolute -top-1 left-1/2 transform -translate-x-1/2 w-2 h-2 sm:w-3 sm:h-3 rounded-full animate-pulse transition-colors duration-300"
              :class="sectionUnderlineDotClasses"
            ></div>
          </div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 md:gap-12">
          <div ref="aboutLeft" class="opacity-0">
            <p class="mb-4 md:mb-6 text-base sm:text-lg" :class="aboutTextClasses">
              I am a motivated Full-Stack Developer and Mobile Developer with experience building
              web applications, real-time systems, and modern user interfaces. I work with Laravel,
              Next.js, Nest.js, PostgreSQL, Redis, and also develop mobile apps using Flutter.
            </p>
            <p class="mb-4 md:mb-6 text-base sm:text-lg" :class="aboutTextClasses">
              I enjoy solving problems, designing systems, and creating efficient platforms such as
              e-management and e-commerce systems. I am passionate about learning new skills,
              working with teams, and delivering good-quality work.
            </p>
            <div class="flex flex-wrap gap-3 md:gap-4 mb-6">
              <div
                v-for="stat in experienceStats"
                :key="stat.label"
                class="p-3 rounded-lg transition-colors duration-300"
                :class="experienceStatClasses"
              >
                <div :class="experienceStatNumberClasses">{{ stat.number }}</div>
                <div class="text-xs sm:text-sm" :class="experienceStatLabelClasses">
                  {{ stat.label }}
                </div>
              </div>
            </div>
          </div>
          <div ref="aboutRight" class="opacity-0">
            <h3 class="text-lg sm:text-xl font-bold mb-3 md:mb-4" :class="competenciesTitleClasses">
              Core Competencies
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 md:gap-4">
              <div
                v-for="skill in coreCompetencies"
                :key="skill.name"
                class="p-3 sm:p-4 rounded-lg transition-colors duration-300"
                :class="competencyCardClasses"
              >
                <div class="font-semibold text-sm sm:text-base" :class="competencyNameClasses">
                  {{ skill.name }}
                </div>
                <div class="text-xs sm:text-sm mt-1" :class="competencyItemsClasses">
                  {{ skill.items.join(', ') }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="py-12 sm:py-16 md:py-20" :class="experienceSectionClasses">
      <div class="container mx-auto px-4 sm:px-6">
        <!-- Title with Icon and Underline -->
        <div class="mb-8 sm:mb-12 text-center opacity-0" ref="experienceTitle">
          <div class="inline-flex items-center justify-center mb-3 sm:mb-4">
            <div
              class="w-8 h-8 sm:w-10 sm:h-10 rounded-full flex items-center justify-center mr-2 sm:mr-3 transition-colors duration-300"
              :class="sectionIconClasses"
            >
              <svg
                class="w-4 h-4 sm:w-5 sm:h-5 text-white"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                />
              </svg>
            </div>
            <h2 class="text-2xl sm:text-3xl font-bold" :class="sectionTitleClasses">
              Work Experience
            </h2>
          </div>
          <div class="relative">
            <div
              class="w-16 sm:w-24 h-1 mx-auto rounded-full transition-colors duration-300"
              :class="sectionUnderlineClasses"
            ></div>
            <div
              class="absolute -top-1 left-1/2 transform -translate-x-1/2 w-2 h-2 sm:w-3 sm:h-3 rounded-full animate-pulse transition-colors duration-300"
              :class="sectionUnderlineDotClasses"
            ></div>
          </div>
        </div>
        <div class="space-y-6 sm:space-y-8 md:space-y-12">
          <div
            v-for="(exp, index) in experiences"
            :key="index"
            :ref="`exp-${index}`"
            class="opacity-0"
          >
            <div
              class="rounded-xl p-4 sm:p-6 shadow-lg transition-colors duration-300"
              :class="experienceCardClasses"
            >
              <div class="flex flex-col md:flex-row justify-between mb-3 sm:mb-4">
                <h3
                  class="text-lg sm:text-xl font-bold mb-2 md:mb-0"
                  :class="experienceTitleClasses"
                >
                  {{ exp.title }}
                </h3>
                <div :class="experiencePeriodClasses">{{ exp.period }}</div>
              </div>
              <p class="mb-4 md:mb-6 text-sm sm:text-base" :class="experienceDescriptionClasses">
                {{ exp.description }}
              </p>
              <div class="flex flex-wrap gap-2 mb-3 sm:mb-4">
                <span
                  v-for="tech in exp.technologies"
                  :key="tech"
                  class="px-2 sm:px-3 py-1 rounded-full text-xs sm:text-sm transition-colors duration-300"
                  :class="experienceTechClasses"
                >
                  {{ tech }}
                </span>
              </div>
              <ul class="space-y-1 sm:space-y-2">
                <li
                  v-for="(detail, detailIndex) in exp.details"
                  :key="detailIndex"
                  class="flex items-start"
                >
                  <div class="mr-2 mt-1" :class="experienceDetailDotClasses">•</div>
                  <div class="text-sm sm:text-base" :class="experienceDetailTextClasses">
                    {{ detail }}
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="py-12 sm:py-16 md:py-20" :class="projectsSectionClasses">
      <div class="container mx-auto px-4 sm:px-6">
        <!-- Title with Icon and Underline -->
        <div class="mb-8 sm:mb-12 text-center opacity-0" ref="projectsTitle">
          <div class="inline-flex items-center justify-center mb-3 sm:mb-4">
            <div
              class="w-8 h-8 sm:w-10 sm:h-10 rounded-full flex items-center justify-center mr-2 sm:mr-3 transition-colors duration-300"
              :class="sectionIconClasses"
            >
              <svg
                class="w-4 h-4 sm:w-5 sm:h-5 text-white"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"
                />
              </svg>
            </div>
            <h2 class="text-2xl sm:text-3xl font-bold" :class="sectionTitleClasses">
              Key Projects
            </h2>
          </div>
          <div class="relative">
            <div
              class="w-16 sm:w-24 h-1 mx-auto rounded-full transition-colors duration-300"
              :class="sectionUnderlineClasses"
            ></div>
            <div
              class="absolute -top-1 left-1/2 transform -translate-x-1/2 w-2 h-2 sm:w-3 sm:h-3 rounded-full animate-pulse transition-colors duration-300"
              :class="sectionUnderlineDotClasses"
            ></div>
          </div>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-8">
          <div
            v-for="project in projects"
            :key="project.id"
            :ref="`project-${project.id}`"
            class="opacity-0 rounded-xl overflow-hidden shadow-lg hover:shadow-2xl transition-all duration-300"
            :class="projectCardClasses"
          >
            <div class="p-4 sm:p-6">
              <div class="font-bold text-lg sm:text-xl mb-1 sm:mb-2" :class="projectTitleClasses">
                {{ project.name }}
              </div>
              <div class="text-sm mb-3 sm:mb-4" :class="projectYearClasses">{{ project.year }}</div>
              <p class="mb-4 sm:mb-6 text-sm sm:text-base" :class="projectDescriptionClasses">
                {{ project.description }}
              </p>
              <div class="flex flex-wrap gap-1 sm:gap-2">
                <span
                  v-for="tech in project.technologies"
                  :key="tech"
                  class="px-2 sm:px-3 py-1 rounded-full text-xs transition-colors duration-300"
                  :class="projectTechClasses"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section id="education" class="py-12 sm:py-16 md:py-20" :class="educationSectionClasses">
      <div class="container mx-auto px-4 sm:px-6">
        <!-- Title with Icon and Underline -->
        <div class="mb-8 sm:mb-12 text-center opacity-0" ref="educationTitle">
          <div class="inline-flex items-center justify-center mb-3 sm:mb-4">
            <div
              class="w-8 h-8 sm:w-10 sm:h-10 rounded-full flex items-center justify-center mr-2 sm:mr-3 transition-colors duration-300"
              :class="sectionIconClasses"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-4 h-4 sm:w-5 sm:h-5 text-white"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5"
                />
              </svg>
            </div>
            <h2 class="text-2xl sm:text-3xl font-bold" :class="sectionTitleClasses">Education</h2>
          </div>
          <div class="relative">
            <div
              class="w-16 sm:w-24 h-1 mx-auto rounded-full transition-colors duration-300"
              :class="sectionUnderlineClasses"
            ></div>
            <div
              class="absolute -top-1 left-1/2 transform -translate-x-1/2 w-2 h-2 sm:w-3 sm:h-3 rounded-full animate-pulse transition-colors duration-300"
              :class="sectionUnderlineDotClasses"
            ></div>
          </div>
        </div>
        <div
          ref="educationContent"
          class="rounded-xl p-4 sm:p-6 md:p-8 shadow-lg opacity-0 transition-colors duration-300"
          :class="educationContentClasses"
        >
          <h3 class="text-xl sm:text-2xl font-bold mb-1 sm:mb-2" :class="educationDegreeClasses">
            Bachelor of Engineering in Information & Communication Technology (ICT)
          </h3>
          <div class="text-sm sm:text-lg mb-4 sm:mb-6" :class="educationInstitutionClasses">
            Institute of Technology of Cambodia (ITC) - 2021 - Present
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6">
            <div
              v-for="year in educationYears"
              :key="year.year"
              class="p-4 sm:p-6 rounded-lg transition-colors duration-300"
              :class="educationYearCardClasses"
            >
              <h4
                class="text-lg sm:text-xl font-bold mb-3 sm:mb-4"
                :class="educationYearTitleClasses"
              >
                {{ year.year }}
              </h4>
              <ul class="space-y-1 sm:space-y-2">
                <li
                  v-for="(course, index) in year.courses"
                  :key="index"
                  class="text-sm sm:text-base"
                  :class="educationCourseClasses"
                >
                  {{ course }}
                </li>
              </ul>
            </div>
          </div>

          <div class="mt-8 sm:mt-10">
            <h3
              class="text-lg sm:text-xl font-bold mb-3 sm:mb-4"
              :class="certificationTitleClasses"
            >
              Certifications & Professional Development
            </h3>
            <div
              class="p-4 sm:p-6 rounded-lg transition-colors duration-300"
              :class="certificationCardClasses"
            >
              <div
                class="font-bold text-base sm:text-lg mb-1 sm:mb-2"
                :class="certificationNameClasses"
              >
                AWS Cloud Computing – Certificate of Completion
              </div>
              <p class="text-sm sm:text-base" :class="certificationDescriptionClasses">
                Online learning in system design, cloud fundamentals, and backend architecture.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-12 sm:py-16 md:py-20" :class="contactSectionClasses">
      <div class="container mx-auto px-4 sm:px-6">
        <!-- Title with Icon and Underline -->
        <div class="mb-8 sm:mb-12 text-center opacity-0" ref="contactTitle">
          <div class="inline-flex items-center justify-center mb-3 sm:mb-4">
            <div
              class="w-8 h-8 sm:w-10 sm:h-10 rounded-full flex items-center justify-center mr-2 sm:mr-3 transition-colors duration-300"
              :class="sectionIconClasses"
            >
              <svg
                class="w-4 h-4 sm:w-5 sm:h-5 text-white"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                />
              </svg>
            </div>
            <h2 class="text-2xl sm:text-3xl font-bold" :class="sectionTitleClasses">Contact</h2>
          </div>
          <div class="relative">
            <div
              class="w-16 sm:w-24 h-1 mx-auto rounded-full transition-colors duration-300"
              :class="sectionUnderlineClasses"
            ></div>
            <div
              class="absolute -top-1 left-1/2 transform -translate-x-1/2 w-2 h-2 sm:w-3 sm:h-3 rounded-full animate-pulse transition-colors duration-300"
              :class="sectionUnderlineDotClasses"
            ></div>
          </div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 md:gap-12">
          <div ref="contactLeft" class="opacity-0">
            <h3 class="text-xl sm:text-2xl font-bold mb-4 sm:mb-6" :class="contactTitleClasses">
              Get In Touch
            </h3>
            <p class="mb-6 md:mb-8 text-sm sm:text-base" :class="contactTextClasses">
              I'm always open to discussing new opportunities, interesting projects, or just having
              a chat about technology.
            </p>

            <div class="space-y-4 sm:space-y-6">
              <div class="flex items-center">
                <div
                  class="p-2 sm:p-3 rounded-lg mr-3 sm:mr-4 transition-colors duration-300"
                  :class="contactIconClasses"
                >
                  <svg
                    class="w-5 h-5 sm:w-6 sm:h-6"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                    ></path>
                  </svg>
                </div>
                <div>
                  <div class="font-bold text-sm sm:text-base" :class="contactLabelClasses">
                    Email
                  </div>
                  <div class="text-sm sm:text-base" :class="contactValueClasses">
                    kimsrenghai@gmail.com
                  </div>
                </div>
              </div>

              <div class="flex items-center">
                <div
                  class="p-2 sm:p-3 rounded-lg mr-3 sm:mr-4 transition-colors duration-300"
                  :class="contactIconClasses"
                >
                  <svg
                    class="w-5 h-5 sm:w-6 sm:h-6"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
                    ></path>
                  </svg>
                </div>
                <div>
                  <div class="font-bold text-sm sm:text-base" :class="contactLabelClasses">
                    Phone
                  </div>
                  <div class="text-sm sm:text-base" :class="contactValueClasses">069-367-***</div>
                </div>
              </div>

              <div class="flex items-center">
                <div
                  class="p-2 sm:p-3 rounded-lg mr-3 sm:mr-4 transition-colors duration-300"
                  :class="contactIconClasses"
                >
                  <svg
                    class="w-5 h-5 sm:w-6 sm:h-6"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                    ></path>
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                    ></path>
                  </svg>
                </div>
                <div>
                  <div class="font-bold text-sm sm:text-base" :class="contactLabelClasses">
                    Location
                  </div>
                  <div class="text-sm sm:text-base" :class="contactValueClasses">
                    Phnom Penh, Cambodia
                  </div>
                </div>
              </div>
            </div>

            <div class="mt-6 sm:mt-8">
              <h4 class="text-lg sm:text-xl font-bold mb-3 sm:mb-4" :class="languagesTitleClasses">
                Languages
              </h4>
              <div class="flex flex-wrap gap-2 sm:gap-4">
                <div
                  v-for="lang in languages"
                  :key="lang.name"
                  class="px-3 sm:px-4 py-2 rounded-lg transition-colors duration-300"
                  :class="languageCardClasses"
                >
                  <div class="font-bold text-sm sm:text-base" :class="languageNameClasses">
                    {{ lang.name }}
                  </div>
                  <div class="text-xs sm:text-sm" :class="languageLevelClasses">
                    {{ lang.level }}
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div ref="contactRight" class="opacity-0">
            <h3 class="text-xl sm:text-2xl font-bold mb-4 sm:mb-6" :class="skillsTitleClasses">
              Skills & Abilities
            </h3>

            <div class="mb-6 sm:mb-8">
              <h4
                class="text-lg sm:text-xl font-bold mb-3 sm:mb-4"
                :class="technicalSkillsTitleClasses"
              >
                Technical Skills
              </h4>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 sm:gap-4">
                <div
                  v-for="skill in technicalSkills"
                  :key="skill.name"
                  class="p-3 sm:p-4 rounded-lg transition-colors duration-300"
                  :class="technicalSkillCardClasses"
                >
                  <div
                    class="font-bold text-sm sm:text-base mb-1 sm:mb-2"
                    :class="skillNameClasses"
                  >
                    {{ skill.name }}
                  </div>
                  <div class="h-2 bg-gray-200 dark:bg-gray-700 rounded-full overflow-hidden">
                    <div
                      class="h-full rounded-full transition-colors duration-300"
                      :class="skillBarClasses"
                      :style="{ width: skill.level + '%' }"
                    ></div>
                  </div>
                </div>
              </div>
            </div>

            <div>
              <h4 class="text-lg sm:text-xl font-bold mb-3 sm:mb-4" :class="softSkillsTitleClasses">
                Soft Skills
              </h4>
              <div class="flex flex-wrap gap-2 sm:gap-3">
                <span
                  v-for="skill in softSkills"
                  :key="skill"
                  class="px-3 sm:px-4 py-1.5 sm:py-2 rounded-full text-sm sm:text-base transition-colors duration-300"
                  :class="softSkillTagClasses"
                >
                  {{ skill }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="py-6 sm:py-8 transition-colors duration-300" :class="footerClasses">
      <div class="container mx-auto px-4 sm:px-6">
        <div class="flex flex-col md:flex-row justify-between items-center">
          <div class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4 md:mb-0">
            <span :class="footerLogoPrimaryClasses">HAI</span>
            <span :class="footerLogoSecondaryClasses"> KIMSRENG</span>
          </div>
          <div class="text-sm sm:text-base mb-3 sm:mb-4 md:mb-0" :class="footerTextClasses">
            &copy; 2025 Portfolio. All rights reserved.
          </div>
          <div class="flex space-x-3 sm:space-x-4">
            <a
              href="https://github.com/Kimsreng28"
              target="_blank"
              class="p-2 sm:p-3 rounded-full transition-all duration-300"
              :class="footerSocialIconClasses"
            >
              <svg class="w-5 h-5 sm:w-6 sm:h-6" fill="currentColor" viewBox="0 0 24 24">
                <path
                  d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                />
              </svg>
            </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import profileImage from '../assets/images/Kimsreng.jpg'

export default {
  name: 'HomeView',
  data() {
    return {
      mobileMenuOpen: false,
      darkMode: true,
      navTransform: 'translateY(0)',
      lastScrollTop: 0,
      isNavbarScrolled: false,
      profileImage: profileImage,
      profileImageLoaded: false,
      quickStats: [
        { number: '10+', label: 'Projects' },
        { number: '2+', label: 'Years Experience' },
        { number: '5+', label: 'Technologies' },
      ],
      experienceStats: [
        { number: '2+', label: 'Years Experience' },
        { number: '10+', label: 'Projects Completed' },
        { number: '5+', label: 'Technologies' },
      ],
      navItems: [
        {
          id: 'home',
          name: 'Home',
          icon: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6',
        },
        {
          id: 'about',
          name: 'About',
          icon: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z',
        },
        {
          id: 'experience',
          name: 'Experience',
          icon: 'M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z',
        },
        {
          id: 'projects',
          name: 'Projects',
          icon: 'M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10',
        },
        {
          id: 'education',
          name: 'Education',
          icon: 'M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5',
        },
        {
          id: 'contact',
          name: 'Contact',
          icon: 'M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z',
        },
      ],
      mainTech: ['Laravel', 'Next.js', 'Nest.js', 'Flutter', 'PostgreSQL'],
      techStack: [
        {
          name: 'Laravel',
          logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Laravel.svg/1200px-Laravel.svg.png',
          category: 'Backend',
        },
        {
          name: 'Next.js',
          logo: 'https://logo.svgcdn.com/devicon/nextjs-original.png',
          category: 'Frontend',
        },
        {
          name: 'NestJS',
          logo: 'https://nestjs.com/img/logo-small.svg',
          category: 'Backend',
        },
        {
          name: 'Node.js',
          logo: 'https://nodejs.org/static/images/logo.svg',
          category: 'Runtime',
        },
        {
          name: 'Vue.js',
          logo: 'https://vuejs.org/images/logo.png',
          category: 'Frontend',
        },
        {
          name: 'React',
          logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/1200px-React-icon.svg.png',
          category: 'Frontend',
        },
        {
          name: 'Flutter',
          logo: 'https://juststickers.in/wp-content/uploads/2019/01/flutter.png',
          category: 'Mobile',
        },
        {
          name: 'PostgreSQL',
          logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Postgresql_elephant.svg/1200px-Postgresql_elephant.svg.png',
          category: 'Database',
        },
        {
          name: 'MySQL',
          logo: 'https://www.mysql.com/common/logos/logo-mysql-170x115.png',
          category: 'Database',
        },
        {
          name: 'Redis',
          logo: 'https://cdn.iconscout.com/icon/free/png-256/free-redis-icon-svg-download-png-1175103.png?f=webp',
          category: 'Cache',
        },
        {
          name: 'Docker',
          logo: 'https://www.docker.com/wp-content/uploads/2022/03/vertical-logo-monochromatic.png',
          category: 'DevOps',
        },
        {
          name: 'Socket.IO',
          logo: 'https://socket.io/images/logo.svg',
          category: 'Real-time',
        },
        {
          name: 'TypeScript',
          logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Typescript_logo_2020.svg/1200px-Typescript_logo_2020.svg.png',
          category: 'Language',
        },
        {
          name: 'Tailwind',
          logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Tailwind_CSS_Logo.svg/1200px-Tailwind_CSS_Logo.svg.png',
          category: 'CSS',
        },
      ],
      sliderAnimation: null,
      coreCompetencies: [
        { name: 'Full-Stack', items: ['Laravel', 'Nest.js', 'Next.js'] },
        { name: 'Database', items: ['PostgreSQL', 'MySQL', 'Prisma'] },
        { name: 'Real-Time', items: ['Socket.IO', 'WebSockets'] },
        { name: 'Mobile', items: ['Flutter'] },
        { name: 'Security', items: ['OAuth2', 'JWT', 'Resend'] },
        { name: 'Payments', items: ['Stripe', 'KHQR Bakong'] },
        { name: 'DevOps', items: ['Redis', 'CI/CD', 'Docker'] },
        { name: 'UI/UX', items: ['Figma'] },
      ],
      experiences: [
        {
          title: 'Full-Stack Developer – E-Management Platform Project',
          period: '2025 - Present',
          description: 'Personal/Academic Project',
          technologies: [
            'Laravel',
            'Next.js',
            'PostgreSQL',
            'Redis',
            'OAuth2',
            'Telegram Bot API',
            'Stripe',
            'KHQR Bakong',
          ],
          details: [
            'Built a full modern E-Management Platform from scratch using professional software architecture',
            'Designed and developed complete management platform with authentication, admin dashboards, and role-based permissions',
            'Integrated Redis for caching and performance optimization',
            'Developed Telegram Bot notification system for real-time alerts',
            'Added multiple payment methods including Stripe, KHQR Bakong, Cash on Delivery',
            'Implemented Chat System for text, image, voice, and calls between users',
          ],
        },
        {
          title: 'Project Developer – Real-Time Quiz App (DICE)',
          period: '2024',
          description: 'Team/Academic Project',
          technologies: ['Vue.js', 'Nest.js', 'Socket.IO', 'Flutter'],
          details: [
            'Developed real-time quiz platform for multiple students to join simultaneously',
            'Built web version using Vue.js and mobile version using Flutter',
            'Implemented socket communication for real-time synchronization',
          ],
        },
        {
          title: 'Project Developer – E-Commerce Platform',
          period: '2024',
          description: 'Team/Academic Project',
          technologies: ['Next.js', 'Nest.js', 'MySQL', 'Go', 'OAuth'],
          details: [
            'Developed e-commerce platform for browsing products and checkout with multiple methods',
            'Implemented multiple roles access (Admin, Vendor, Customer)',
            'Integrated microservice file storage using Go',
            'Designed responsive UI using Next.js for multiple devices',
          ],
        },
      ],
      projects: [
        {
          id: 1,
          name: 'E-Management System',
          year: '2025',
          description:
            'Complete management platform with payment integration, caching, and automation.',
          technologies: ['Laravel', 'Next.js', 'PostgreSQL', 'Redis', 'Stripe'],
        },
        {
          id: 2,
          name: 'Real-Time Quiz App',
          year: '2024',
          description: 'Web and mobile app with socket-based real-time communication.',
          technologies: ['Vue.js', 'Nest.js', 'Socket.IO', 'Flutter'],
        },
        {
          id: 3,
          name: 'E-Commerce Platform',
          year: '2024',
          description: 'Full-featured e-commerce with multi-role access and microservices.',
          technologies: ['Next.js', 'Nest.js', 'MySQL', 'Go', 'OAuth'],
        },
        {
          id: 4,
          name: 'Java Swing Game',
          year: '2023',
          description: 'Desktop adventure game with OOP design and game logic.',
          technologies: ['Java', 'Swing', 'OOP'],
        },
      ],
      educationYears: [
        {
          year: 'Foundation',
          courses: ['Mathematics', 'Physics', 'History', 'French', 'Python'],
        },
        {
          year: 'Year 2',
          courses: ['Computer Architecture', 'Data Structures', 'Probability', 'C/C++'],
        },
        {
          year: 'Year 3',
          courses: ['Algorithms', 'Networking', 'OOP with Java', 'Databases', 'Web Design'],
        },
        {
          year: 'Year 4',
          courses: [
            'Network Design',
            'System Administration',
            'Vue & Next.js',
            'NestJS',
            'Laravel',
            'Flutter',
            'DevOps',
          ],
        },
        {
          year: 'Year 5',
          courses: ['AI', 'NLP', 'Network Security', 'Cloud Computing AWS'],
        },
      ],
      languages: [
        { name: 'Khmer', level: 'Native' },
        { name: 'English', level: 'Intermediate' },
        { name: 'French', level: 'Intermediate' },
      ],
      technicalSkills: [
        { name: 'Laravel', level: 90 },
        { name: 'Next.js', level: 85 },
        { name: 'Nest.js', level: 80 },
        { name: 'Flutter', level: 75 },
        { name: 'PostgreSQL', level: 85 },
        { name: 'Vue.js', level: 80 },
      ],
      softSkills: [
        'Communication',
        'Teamwork',
        'Leadership',
        'Problem-Solving',
        'Critical Thinking',
        'Time Management',
        'Creativity',
        'Adaptability',
      ],
    }
  },
  computed: {
    modeClasses() {
      return this.darkMode ? 'dark bg-gray-900 text-white' : 'bg-gray-50 text-gray-900'
    },
    textColor() {
      return this.darkMode ? 'text-white' : 'text-gray-900'
    },
    navClasses() {
      if (this.isNavbarScrolled) {
        return this.darkMode
          ? 'bg-gray-900/95 backdrop-blur-lg border-gray-800/50 shadow-xl'
          : 'bg-white/95 backdrop-blur-lg border-gray-200/50 shadow-xl'
      }
      return this.darkMode
        ? 'bg-transparent backdrop-blur-lg border-transparent'
        : 'bg-transparent backdrop-blur-lg border-transparent'
    },
    logoClasses() {
      return this.darkMode
        ? 'bg-gradient-to-br from-blue-500 to-blue-700 text-white'
        : 'bg-gradient-to-br from-blue-400 to-blue-600 text-white'
    },
    logoTextClasses() {
      return this.darkMode
        ? 'text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600'
        : 'text-transparent bg-clip-text bg-gradient-to-r from-blue-500 to-blue-700'
    },
    navContainerClasses() {
      return this.darkMode
        ? 'bg-gray-800/50 border-gray-700/50'
        : 'bg-gray-100/50 border-gray-300/50'
    },
    navLinkClasses() {
      return this.darkMode ? 'hover:bg-gray-700/50' : 'hover:bg-gray-200/50'
    },
    navIconClasses() {
      return this.darkMode
        ? 'text-blue-400 group-hover:text-blue-300'
        : 'text-blue-500 group-hover:text-blue-600'
    },
    navTextClasses() {
      return this.darkMode
        ? 'text-gray-300 group-hover:text-white'
        : 'text-gray-600 group-hover:text-gray-900'
    },
    navIndicatorClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-400 to-blue-600'
        : 'bg-gradient-to-r from-blue-500 to-blue-700'
    },
    themeToggleClasses() {
      return this.darkMode
        ? 'bg-gray-800/80 hover:bg-gray-700/80 border-gray-700/50'
        : 'bg-gray-100/80 hover:bg-gray-200/80 border-gray-300/50'
    },
    mobileMenuButtonClasses() {
      return this.darkMode
        ? 'bg-gray-800/80 hover:bg-gray-700/80 border-gray-700/50'
        : 'bg-gray-100/80 hover:bg-gray-200/80 border-gray-300/50'
    },
    mobileMenuLineClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-400 to-blue-300'
        : 'bg-gradient-to-r from-blue-500 to-blue-600'
    },
    mobileMenuClasses() {
      return this.darkMode ? 'bg-gray-800/95 border-gray-700/50' : 'bg-white/95 border-gray-200/50'
    },
    mobileNavLinkClasses() {
      return this.darkMode ? 'hover:bg-gray-700/50' : 'hover:bg-gray-100/50'
    },
    mobileNavIconContainerClasses() {
      return this.darkMode
        ? 'bg-gray-900/50 group-hover:bg-gradient-to-br from-blue-900/30 to-blue-700/30'
        : 'bg-gray-100/50 group-hover:bg-gradient-to-br from-blue-100/50 to-blue-200/50'
    },
    mobileNavIconClasses() {
      return this.darkMode
        ? 'text-blue-400 group-hover:text-blue-300'
        : 'text-blue-500 group-hover:text-blue-600'
    },
    mobileNavTextClasses() {
      return this.darkMode
        ? 'text-gray-300 group-hover:text-white'
        : 'text-gray-600 group-hover:text-gray-900'
    },
    mobileNavArrowClasses() {
      return this.darkMode
        ? 'text-gray-500 group-hover:text-blue-400'
        : 'text-gray-400 group-hover:text-blue-500'
    },
    mobileMenuFooterClasses() {
      return this.darkMode ? 'border-gray-700/50' : 'border-gray-300/50'
    },
    socialIconClasses() {
      return this.darkMode
        ? 'bg-gray-900/50 hover:bg-gray-700/50'
        : 'bg-gray-100/50 hover:bg-gray-200/50'
    },
    socialIconSvgClasses() {
      return this.darkMode ? 'text-gray-400 hover:text-white' : 'text-gray-500 hover:text-gray-900'
    },
    heroBgCircle1() {
      return this.darkMode ? 'bg-blue-500' : 'bg-blue-300'
    },
    heroBgCircle2() {
      return this.darkMode ? 'bg-blue-700' : 'bg-blue-400'
    },
    heroBgCircle3() {
      return this.darkMode ? 'bg-blue-400' : 'bg-blue-200'
    },
    heroBadgeClasses() {
      return this.darkMode ? 'bg-blue-600/20' : 'bg-blue-100/50'
    },
    heroBadgeTextClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-600'
    },
    heroTitleClasses() {
      return this.darkMode
        ? 'text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600'
        : 'text-transparent bg-clip-text bg-gradient-to-r from-blue-500 to-blue-700'
    },
    heroSubtitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    heroSubtitleSpan1() {
      return this.darkMode ? 'text-blue-300' : 'text-blue-500'
    },
    heroSubtitleSpan2() {
      return this.darkMode ? 'text-blue-200' : 'text-blue-400'
    },
    heroTextClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    quickStatsClasses() {
      return this.darkMode ? 'bg-gray-800/50 border-gray-700' : 'bg-white/50 border-gray-300'
    },
    quickStatsNumberClasses() {
      return this.darkMode
        ? 'text-blue-400 font-bold text-xl sm:text-2xl'
        : 'text-blue-500 font-bold text-xl sm:text-2xl'
    },
    quickStatsLabelClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    techStackTitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    techStackItemClasses() {
      return this.darkMode
        ? 'bg-gray-800/70 hover:bg-blue-900/30 border-gray-700 hover:border-blue-500'
        : 'bg-gray-100/70 hover:bg-blue-100/50 border-gray-300 hover:border-blue-400'
    },
    techStackTextClasses() {
      return this.darkMode
        ? 'text-gray-300 group-hover:text-blue-300'
        : 'text-gray-700 group-hover:text-blue-600'
    },
    ctaButtonPrimaryClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white'
        : 'bg-gradient-to-r from-blue-500 to-blue-600 hover:from-blue-600 hover:to-blue-700 text-white'
    },
    ctaButtonSecondaryClasses() {
      return this.darkMode
        ? 'bg-gray-800/70 hover:bg-gray-700/70 border-gray-700 hover:border-gray-600 text-gray-300'
        : 'bg-gray-100/70 hover:bg-gray-200/70 border-gray-300 hover:border-gray-400 text-gray-700'
    },
    ctaButtonTertiaryClasses() {
      return this.darkMode
        ? 'bg-gray-800/30 hover:bg-gray-700/50 border-gray-700/50 hover:border-gray-600/70 text-gray-300'
        : 'bg-gray-100/30 hover:bg-gray-200/50 border-gray-300/50 hover:border-gray-400/70 text-gray-700'
    },
    profileRingClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-500 to-blue-700'
        : 'bg-gradient-to-r from-blue-400 to-blue-600'
    },
    profileBgClasses() {
      return this.darkMode
        ? 'bg-gradient-to-br from-blue-900 via-gray-900 to-blue-950'
        : 'bg-gradient-to-br from-blue-50 via-gray-50 to-blue-100'
    },
    profileFallbackClasses() {
      return this.darkMode
        ? 'bg-gradient-to-br from-blue-800 to-blue-900'
        : 'bg-gradient-to-br from-blue-100 to-blue-200'
    },
    profileInitialsClasses() {
      return this.darkMode ? 'text-white opacity-80' : 'text-blue-900 opacity-80'
    },
    profileTitleClasses() {
      return this.darkMode ? 'text-blue-200' : 'text-blue-700'
    },
    floatingBadgeClasses() {
      return this.darkMode ? 'bg-blue-600' : 'bg-blue-500'
    },
    infoCardClasses() {
      return this.darkMode ? 'bg-gray-800/80 border-gray-700/50' : 'bg-white/80 border-gray-300/50'
    },
    infoCardTitleClasses() {
      return this.darkMode ? 'text-white' : 'text-gray-900'
    },
    infoCardSubtitleClasses() {
      return this.darkMode ? 'text-blue-300' : 'text-blue-500'
    },
    infoCardIconClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-600 to-blue-800'
        : 'bg-gradient-to-r from-blue-500 to-blue-700'
    },
    infoCardTextClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    infoCardBorderClasses() {
      return this.darkMode ? 'border-gray-700/50' : 'border-gray-300/50'
    },
    infoCardLinkClasses() {
      return this.darkMode
        ? 'text-blue-400 hover:text-blue-300'
        : 'text-blue-500 hover:text-blue-600'
    },
    infoCardDividerClasses() {
      return this.darkMode ? 'text-gray-600' : 'text-gray-400'
    },
    profileDeco1() {
      return this.darkMode ? 'bg-blue-500' : 'bg-blue-300'
    },
    profileDeco2() {
      return this.darkMode ? 'bg-blue-700' : 'bg-blue-400'
    },
    scrollIndicatorClasses() {
      return this.darkMode
        ? 'text-gray-400 hover:text-blue-400'
        : 'text-gray-500 hover:text-blue-500'
    },
    techSliderClasses() {
      return this.darkMode ? 'bg-gray-800/50' : 'bg-gray-100/50'
    },
    sectionIconClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-500 to-blue-600'
        : 'bg-gradient-to-r from-blue-400 to-blue-500'
    },
    sectionTitleClasses() {
      return this.darkMode ? 'text-white' : 'text-gray-900'
    },
    sectionSubtitleClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-600'
    },
    techSliderGradientLeft() {
      return this.darkMode
        ? 'bg-gradient-to-r from-gray-800 to-transparent'
        : 'bg-gradient-to-r from-gray-100 to-transparent'
    },
    techSliderGradientRight() {
      return this.darkMode
        ? 'bg-gradient-to-l from-gray-800 to-transparent'
        : 'bg-gradient-to-l from-gray-100 to-transparent'
    },
    techCardClasses() {
      return this.darkMode
        ? 'bg-gradient-to-br from-gray-900 to-gray-800 border-gray-700 group-hover:border-blue-500/50 group-hover:shadow-blue-500/10'
        : 'bg-gradient-to-br from-gray-50 to-white border-gray-300 group-hover:border-blue-400/50 group-hover:shadow-blue-400/10'
    },
    techNameClasses() {
      return this.darkMode
        ? 'text-white group-hover:text-blue-300'
        : 'text-gray-900 group-hover:text-blue-600'
    },
    aboutSectionClasses() {
      return this.darkMode ? 'bg-gray-800' : 'bg-gray-100'
    },
    sectionUnderlineClasses() {
      return this.darkMode
        ? 'bg-gradient-to-r from-blue-400 via-blue-500 to-blue-600'
        : 'bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700'
    },
    sectionUnderlineDotClasses() {
      return this.darkMode ? 'bg-blue-400' : 'bg-blue-500'
    },
    aboutTextClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    experienceStatClasses() {
      return this.darkMode ? 'bg-gray-700' : 'bg-gray-200'
    },
    experienceStatNumberClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    experienceStatLabelClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    competenciesTitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    competencyCardClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-white'
    },
    competencyNameClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    competencyItemsClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-600'
    },
    experienceSectionClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-gray-50'
    },
    experienceCardClasses() {
      return this.darkMode ? 'bg-gray-800' : 'bg-white'
    },
    experienceTitleClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    experiencePeriodClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-500'
    },
    experienceDescriptionClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    experienceTechClasses() {
      return this.darkMode ? 'bg-blue-900/50 text-blue-300' : 'bg-blue-100 text-blue-700'
    },
    experienceDetailDotClasses() {
      return this.darkMode ? 'text-blue-500' : 'text-blue-600'
    },
    experienceDetailTextClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    projectsSectionClasses() {
      return this.darkMode ? 'bg-gray-800' : 'bg-gray-100'
    },
    projectCardClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-white'
    },
    projectTitleClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    projectYearClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-500'
    },
    projectDescriptionClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    projectTechClasses() {
      return this.darkMode ? 'bg-gray-800 text-blue-300' : 'bg-gray-100 text-blue-600'
    },
    educationSectionClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-gray-50'
    },
    educationContentClasses() {
      return this.darkMode ? 'bg-gray-800' : 'bg-white'
    },
    educationDegreeClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    educationInstitutionClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-600'
    },
    educationYearCardClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-gray-100'
    },
    educationYearTitleClasses() {
      return this.darkMode ? 'text-blue-300' : 'text-blue-600'
    },
    educationCourseClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    certificationTitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    certificationCardClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-gray-100'
    },
    certificationNameClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    certificationDescriptionClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    contactSectionClasses() {
      return this.darkMode ? 'bg-gray-800' : 'bg-gray-100'
    },
    contactTitleClasses() {
      return this.darkMode ? 'text-white' : 'text-gray-900'
    },
    contactTextClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    contactIconClasses() {
      return this.darkMode ? 'bg-blue-600' : 'bg-blue-500'
    },
    contactLabelClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    contactValueClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-600'
    },
    languagesTitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    languageCardClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-white'
    },
    languageNameClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    languageLevelClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-600'
    },
    skillsTitleClasses() {
      return this.darkMode ? 'text-white' : 'text-gray-900'
    },
    technicalSkillsTitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    technicalSkillCardClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-white'
    },
    skillNameClasses() {
      return this.darkMode ? 'text-blue-400' : 'text-blue-500'
    },
    skillBarClasses() {
      return this.darkMode ? 'bg-blue-600' : 'bg-blue-500'
    },
    softSkillsTitleClasses() {
      return this.darkMode ? 'text-gray-300' : 'text-gray-700'
    },
    softSkillTagClasses() {
      return this.darkMode ? 'bg-blue-900/50 text-blue-300' : 'bg-blue-100 text-blue-700'
    },
    footerClasses() {
      return this.darkMode ? 'bg-gray-900' : 'bg-gray-800'
    },
    footerLogoPrimaryClasses() {
      return this.darkMode ? 'text-blue-500' : 'text-blue-400'
    },
    footerLogoSecondaryClasses() {
      return this.darkMode ? 'text-white' : 'text-gray-100'
    },
    footerTextClasses() {
      return this.darkMode ? 'text-gray-400' : 'text-gray-300'
    },
    footerSocialIconClasses() {
      return this.darkMode
        ? 'bg-gray-800 hover:bg-gray-700 text-gray-400 hover:text-white'
        : 'bg-gray-700 hover:bg-gray-600 text-gray-300 hover:text-white'
    },
  },
  methods: {
    toggleTheme() {
      this.darkMode = !this.darkMode
      if (this.darkMode) {
        document.documentElement.classList.add('dark')
      } else {
        document.documentElement.classList.remove('dark')
      }
    },
    scrollTo(sectionId) {
      const element = document.getElementById(sectionId)
      if (element) {
        window.scrollTo({
          top: element.offsetTop - 80,
          behavior: 'smooth',
        })
      }
    },
    scrollToAndCloseMenu(sectionId) {
      this.scrollTo(sectionId)
      this.mobileMenuOpen = false
    },
    handleScroll() {
      const scrollTop = window.pageYOffset || document.documentElement.scrollTop

      // Update navbar scrolled state
      this.isNavbarScrolled = scrollTop > 50

      // Handle hide/show on scroll
      if (scrollTop > 100) {
        if (scrollTop > this.lastScrollTop) {
          // Scrolling down - hide navbar
          this.navTransform = 'translateY(-100%)'
        } else {
          // Scrolling up - show navbar
          this.navTransform = 'translateY(0)'
        }
      } else {
        this.navTransform = 'translateY(0)'
      }

      this.lastScrollTop = scrollTop
    },
    initHeroAnimation() {
      gsap.fromTo(
        this.$refs.leftContent,
        { opacity: 0, y: 50 },
        {
          opacity: 1,
          y: 0,
          duration: 1.2,
          ease: 'power3.out',
          delay: 0.3,
        },
      )

      gsap.fromTo(
        this.$refs.rightContent,
        { opacity: 0, y: 50, scale: 0.95 },
        {
          opacity: 1,
          y: 0,
          scale: 1,
          duration: 1.2,
          ease: 'power3.out',
          delay: 0.6,
        },
      )

      if (this.$refs.scrollIndicator) {
        gsap.fromTo(
          this.$refs.scrollIndicator,
          { opacity: 0 },
          {
            opacity: 1,
            duration: 1,
            delay: 1.5,
          },
        )
      }
    },
    initScrollAnimations() {
      gsap.registerPlugin(ScrollTrigger)

      this.$nextTick(() => {
        const sectionTitles = [
          this.$refs.aboutTitle,
          this.$refs.experienceTitle,
          this.$refs.projectsTitle,
          this.$refs.educationTitle,
          this.$refs.contactTitle,
        ]

        sectionTitles.forEach((title) => {
          if (title) {
            gsap.fromTo(
              title,
              { opacity: 0, y: 30 },
              {
                opacity: 1,
                y: 0,
                duration: 0.8,
                scrollTrigger: {
                  trigger: title,
                  start: 'top 80%',
                  once: true,
                },
              },
            )
          }
        })

        const contentSections = [
          { element: this.$refs.aboutLeft, delay: 0 },
          { element: this.$refs.aboutRight, delay: 0.2 },
          { element: this.$refs.educationContent, delay: 0 },
          { element: this.$refs.contactLeft, delay: 0 },
          { element: this.$refs.contactRight, delay: 0.2 },
        ]

        contentSections.forEach((section) => {
          if (section.element) {
            gsap.fromTo(
              section.element,
              { opacity: 0, y: 30 },
              {
                opacity: 1,
                y: 0,
                duration: 0.8,
                delay: section.delay,
                scrollTrigger: {
                  trigger: section.element,
                  start: 'top 75%',
                  once: true,
                },
              },
            )
          }
        })

        this.experiences.forEach((_, index) => {
          if (this.$refs[`exp-${index}`]) {
            const element = this.$refs[`exp-${index}`][0]
            if (element) {
              gsap.fromTo(
                element,
                { opacity: 0, y: 30 },
                {
                  opacity: 1,
                  y: 0,
                  duration: 0.8,
                  delay: index * 0.1,
                  scrollTrigger: {
                    trigger: element,
                    start: 'top 75%',
                    once: true,
                  },
                },
              )
            }
          }
        })

        this.projects.forEach((project, index) => {
          if (this.$refs[`project-${project.id}`]) {
            const element = this.$refs[`project-${project.id}`][0]
            if (element) {
              gsap.fromTo(
                element,
                { opacity: 0, y: 30, scale: 0.95 },
                {
                  opacity: 1,
                  y: 0,
                  scale: 1,
                  duration: 0.8,
                  delay: index * 0.1,
                  scrollTrigger: {
                    trigger: element,
                    start: 'top 75%',
                    once: true,
                  },
                },
              )
            }
          }
        })

        setTimeout(() => {
          ScrollTrigger.refresh()
        }, 1000)
      })
    },
  },
  mounted() {
    // Set initial theme based on system preference
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
      this.darkMode = true
      document.documentElement.classList.add('dark')
    } else {
      this.darkMode = false
      document.documentElement.classList.remove('dark')
    }

    // Add scroll event listener
    window.addEventListener('scroll', this.handleScroll)

    const img = new Image()
    img.src = this.profileImage
    img.onload = () => {
      this.profileImageLoaded = true
    }
    img.onerror = () => {
      this.profileImageLoaded = false
      console.error('Failed to preload profile image at:', this.profileImage)
    }

    this.$nextTick(() => {
      this.initHeroAnimation()

      setTimeout(() => {
        this.initScrollAnimations()
      }, 500)
    })

    window.addEventListener('resize', () => {
      ScrollTrigger.refresh()
    })

    document.addEventListener('visibilitychange', () => {
      if (this.sliderAnimation) {
        if (document.hidden) {
          this.sliderAnimation.pause()
        } else {
          this.sliderAnimation.play()
        }
      }
    })
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll)
  },
}
</script>

<style>
/* Custom animations */
@keyframes spin-slow {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.animate-spin-slow {
  animation: spin-slow linear infinite;
}

/* Ensure proper spacing */
html {
  scroll-behavior: smooth;
}

/* Mobile menu fix */
@media (max-width: 768px) {
  #home {
    padding-top: 100px;
  }
}

/* Profile image container fix */
.relative .absolute.inset-0 {
  z-index: 1;
}

.relative .absolute.inset-2 {
  z-index: 2;
}

/* Title underline animation */
@keyframes slideIn {
  from {
    width: 0;
  }
  to {
    width: 6rem;
  }
}

.title-underline {
  animation: slideIn 0.8s ease-out forwards;
}

/* Section icon animation */
@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-5px);
  }
}

.section-icon {
  animation: float 3s ease-in-out infinite;
}

/* Nav link hover effects */
.nav-link:hover span:last-child {
  width: 2rem;
}

/* Mobile nav link animation */
.mobile-nav-link {
  animation: slideInRight 0.3s ease-out forwards;
  animation-delay: calc(var(--i) * 0.05s);
  opacity: 0;
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Smooth transitions for navbar */
nav {
  transition: all 0.3s ease;
}

/* Logo icon hover effect */
nav .logo-icon {
  transition: all 0.3s ease;
}

nav:hover .logo-icon {
  transform: rotate(15deg);
}

/* Gradient text animation */
.gradient-text {
  background: linear-gradient(90deg, #60a5fa, #3b82f6, #1d4ed8);
  background-size: 200% auto;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 3s linear infinite;
}

@keyframes gradient {
  0% {
    background-position: 0% center;
  }
  100% {
    background-position: 200% center;
  }
}

/* Custom infinite scroll animation */
@keyframes infinite-scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.animate-infinite-scroll {
  animation: infinite-scroll 30s linear infinite;
}

/* Pause animation on hover */
.flex.overflow-hidden:hover .animate-infinite-scroll {
  animation-play-state: paused;
}

/* Smooth transition for items */
.group {
  transition: transform 0.3s ease;
}

.group:hover {
  transform: translateY(-5px);
}

/* Optional: Add pulse animation to logos */
@keyframes pulse-glow {
  0%,
  100% {
    filter: brightness(100%);
  }
  50% {
    filter: brightness(120%);
  }
}

.group:hover img {
  animation: pulse-glow 1.5s ease-in-out infinite;
}

/* Responsive adjustments */
@media (max-width: 640px) {
  .animate-infinite-scroll {
    animation-duration: 20s;
  }

  .container {
    padding-left: 1rem;
    padding-right: 1rem;
  }
}

@media (max-width: 768px) {
  .animate-infinite-scroll {
    animation-duration: 25s;
  }

  h1 {
    font-size: 2.5rem;
  }

  h2 {
    font-size: 2rem;
  }
}

/* Print styles */
@media print {
  .no-print {
    display: none;
  }

  body {
    color: #000;
    background: #fff;
  }

  a {
    color: #000;
    text-decoration: none;
  }
}

@media (max-width: 475px) {
  /* Extra small screen adjustments */
  .text-lg {
    font-size: 1.125rem;
    line-height: 1.75rem;
  }

  .logo-icon {
    width: 2rem;
    height: 2rem;
  }
}
/* Khmer flower floating animation */
@keyframes flower-float {
  0%,
  100% {
    transform: translateY(0) rotate(var(--rotation));
  }
  50% {
    transform: translateY(-5px) rotate(var(--rotation));
  }
}

.khmer-flower {
  animation: flower-float 3s ease-in-out infinite;
}

/* Khmer border rotation animation */
@keyframes khmer-pattern-rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.khmer-border {
  animation: khmer-pattern-rotate 20s linear infinite;
}

/* Badge floating animation */
@keyframes badge-float {
  0%,
  100% {
    transform: translateY(0) rotate(var(--badge-rotation, 0deg));
  }
  50% {
    transform: translateY(-3px) rotate(var(--badge-rotation, 0deg));
  }
}

.badge-float {
  --badge-rotation: 0deg;
  animation: badge-float 4s ease-in-out infinite;
}

.badge-float:nth-child(1) {
  --badge-rotation: 6deg;
}

.badge-float:nth-child(2) {
  --badge-rotation: -6deg;
}

.badge-dot {
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%,
  100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.7;
    transform: scale(1.1);
  }
}

/* Corner element animation */
@keyframes corner-glow {
  0%,
  100% {
    opacity: 0.8;
  }
  50% {
    opacity: 1;
  }
}

.corner-decoration {
  animation: corner-glow 2s ease-in-out infinite;
}

/* Pulse animation for decorative elements */
@keyframes horizontal-pulse {
  0%,
  100% {
    transform: scaleX(1);
    opacity: 0.8;
  }
  50% {
    transform: scaleX(1.2);
    opacity: 1;
  }
}

.pulse-element {
  animation: horizontal-pulse 3s ease-in-out infinite;
}

/* Profile image container glow effect */
@keyframes profile-glow {
  0%,
  100% {
    box-shadow: 0 0 20px rgba(217, 119, 6, 0.3);
  }
  50% {
    box-shadow: 0 0 30px rgba(217, 119, 6, 0.5);
  }
}

/* Add this class to the main container if you want glow effect */
.profile-glow {
  animation: profile-glow 4s ease-in-out infinite;
}

/* Star animation */
@keyframes star-twinkle {
  0%,
  100% {
    opacity: 0.7;
    transform: scale(1) rotate(0deg);
  }
  50% {
    opacity: 1;
    transform: scale(1.2) rotate(180deg);
  }
}

.star-decoration {
  animation: star-twinkle 3s ease-in-out infinite;
}

/* Optional: Add more stars in diagonal positions */
@keyframes star-drift {
  0% {
    transform: translate(0, 0) rotate(0deg);
  }
  25% {
    transform: translate(2px, -2px) rotate(90deg);
  }
  50% {
    transform: translate(0, 0) rotate(180deg);
  }
  75% {
    transform: translate(-2px, 2px) rotate(270deg);
  }
  100% {
    transform: translate(0, 0) rotate(360deg);
  }
}

.star-drift {
  animation: star-drift 10s linear infinite;
}
</style>
