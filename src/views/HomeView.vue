<template>
  <div
    class="min-h-screen overflow-x-hidden bg-white text-gray-900 dark:bg-gray-950 dark:text-white transition-colors duration-300"
  >
    <!-- Scroll Progress -->
    <div class="fixed top-0 left-0 right-0 h-[3px] z-[70] pointer-events-none">
      <div
        class="h-full origin-left bg-gradient-to-r from-blue-500 via-blue-400 to-cyan-300"
        :style="{ transform: `scaleX(${scrollProgress})` }"
      ></div>
    </div>

    <!-- Navigation -->
    <header
      class="fixed inset-x-0 top-0 z-[60] transition-all duration-300"
      :class="
        isScrolled
          ? 'bg-white/90 dark:bg-gray-950/90 backdrop-blur-lg shadow-lg border-b border-gray-200 dark:border-gray-800'
          : 'bg-transparent border-b border-transparent'
      "
    >
      <div class="container mx-auto px-5 sm:px-7 h-[76px] flex items-center justify-between">
        <a href="#home" @click.prevent="scrollTo('home')" class="flex items-center gap-3">
          <img
            src="../assets/images/logo_darkBlue.png"
            alt="DRDC"
            class="h-8 sm:h-10 w-auto dark:hidden"
          />
          <img
            src="../assets/images/logo_white.png"
            alt="DRDC"
            class="hidden h-8 sm:h-10 w-auto dark:block"
          />
          <span class="hidden sm:block leading-tight">
            <b class="block font-bold tracking-wide">HAI KIMSRENG</b>
            <span
              class="block text-[10.5px] uppercase tracking-[0.16em] text-gray-500 dark:text-gray-400"
              >Full Stack Developer</span
            >
          </span>
        </a>

        <nav class="hidden xl:flex items-center gap-7">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="'#' + item.id"
            @click.prevent="scrollTo(item.id)"
            class="relative text-sm font-medium text-gray-700 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-300 nav-link"
          >
            {{ item.name }}
          </a>
        </nav>

        <div class="flex items-center gap-3">
          <!-- Theme Toggle -->
          <button
            @click="toggleTheme"
            class="w-10 h-10 sm:w-11 sm:h-11 rounded-full flex items-center justify-center border shadow-lg bg-white/80 border-gray-300 hover:bg-gray-200 dark:bg-gray-800/80 dark:border-gray-700 dark:hover:bg-gray-700 transition-all duration-300"
            aria-label="Toggle theme"
          >
            <svg
              v-if="darkMode"
              class="w-5 h-5 text-yellow-300"
              fill="currentColor"
              viewBox="0 0 20 20"
            >
              <path
                fill-rule="evenodd"
                d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
                clip-rule="evenodd"
              />
            </svg>
            <svg v-else class="w-5 h-5 text-gray-700" fill="currentColor" viewBox="0 0 20 20">
              <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
            </svg>
          </button>

          <a
            href="#contact"
            @click.prevent="scrollTo('contact')"
            class="hidden md:inline-flex items-center gap-2 px-5 py-2.5 rounded-xl bg-blue-600 hover:bg-blue-500 text-white text-sm font-semibold shadow-lg hover:-translate-y-0.5 transition-all duration-300"
          >
            Let's Connect
          </a>

          <!-- Mobile Menu Button -->
          <button
            @click="mobileMenuOpen = !mobileMenuOpen"
            class="xl:hidden w-10 h-10 sm:w-11 sm:h-11 rounded-xl flex flex-col items-center justify-center gap-1.5 border shadow-lg bg-white border-gray-300 dark:bg-gray-800 dark:border-gray-700"
            aria-label="Toggle menu"
          >
            <span
              class="w-5 h-0.5 rounded-full bg-blue-500 transition-all duration-300"
              :class="mobileMenuOpen ? 'translate-y-2 rotate-45' : ''"
            ></span>
            <span
              class="w-5 h-0.5 rounded-full bg-blue-500 transition-all duration-300"
              :class="mobileMenuOpen ? 'opacity-0' : ''"
            ></span>
            <span
              class="w-5 h-0.5 rounded-full bg-blue-500 transition-all duration-300"
              :class="mobileMenuOpen ? '-translate-y-2 -rotate-45' : ''"
            ></span>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div
        v-if="mobileMenuOpen"
        class="xl:hidden mx-4 mt-2 p-4 rounded-2xl border shadow-2xl bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-800"
      >
        <a
          v-for="item in navItems"
          :key="item.id"
          :href="'#' + item.id"
          @click.prevent="scrollTo(item.id)"
          class="block px-3 py-3 rounded-lg font-medium hover:bg-blue-50 hover:text-blue-600 dark:hover:bg-gray-800 dark:hover:text-blue-400"
        >
          {{ item.name }}
        </a>
      </div>
    </header>

    <!-- Hero -->
    <section id="home" class="relative min-h-screen flex items-center pt-28 pb-24 overflow-hidden">
      <div class="absolute inset-0 pointer-events-none">
        <div
          class="absolute top-1/4 left-1/4 w-72 h-72 rounded-full blur-3xl opacity-20 bg-blue-500 animate-pulse"
        ></div>
        <div
          class="absolute bottom-1/4 right-1/4 w-96 h-96 rounded-full blur-3xl opacity-10 bg-blue-700 animate-pulse"
        ></div>
      </div>

      <div
        class="container mx-auto px-5 sm:px-7 relative z-10 grid lg:grid-cols-2 gap-14 items-center"
      >
        <div>
          <p
            class="rise inline-flex items-center gap-2 px-4 py-2 rounded-full text-xs font-semibold uppercase tracking-[0.18em] bg-blue-100 text-blue-700 dark:bg-blue-600/20 dark:text-blue-400"
            style="animation-delay: 0.2s"
          >
            ❖ Full Stack Developer • DRDC
          </p>

          <h1
            class="rise mt-6 text-[clamp(38px,5.6vw,68px)] font-bold leading-[1.08] tracking-tight"
            style="animation-delay: 0.3s"
          >
            I learn that build
            <span class="relative inline-block text-blue-600 dark:text-blue-400"
              >drone &amp; automation</span
            >
            systems that work.
          </h1>

          <p
            class="rise mt-6 max-w-xl text-lg text-gray-600 dark:text-gray-300"
            style="animation-delay: 0.5s"
          >
            Team Lead at DRDC. I lead the team on GCS Drone Delivery, DRDT and DRDC projects, and
            manage the servers they run on.
          </p>

          <div class="rise mt-8 flex flex-wrap gap-4" style="animation-delay: 0.65s">
            <a
              href="#projects"
              @click.prevent="scrollTo('projects')"
              class="inline-flex items-center gap-2 px-6 py-3.5 rounded-xl bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-500 hover:to-blue-600 text-white font-semibold shadow-lg hover:-translate-y-0.5 transition-all duration-300"
            >
              View My Projects
              <svg
                class="w-4 h-4"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M5 12h14m-6-6l6 6-6 6" />
              </svg>
            </a>
            <a
              href="#contact"
              @click.prevent="scrollTo('contact')"
              class="inline-flex items-center gap-2 px-6 py-3.5 rounded-xl border font-semibold bg-white border-gray-300 text-gray-800 hover:border-blue-500 hover:text-blue-600 dark:bg-gray-800/60 dark:border-gray-700 dark:text-gray-200 dark:hover:border-blue-500 dark:hover:text-blue-400 hover:-translate-y-0.5 transition-all duration-300"
            >
              Contact Me
            </a>
          </div>

          <div
            class="rise mt-8 flex flex-wrap gap-x-6 gap-y-3 text-sm text-gray-600 dark:text-gray-400"
            style="animation-delay: 0.8s"
          >
            <span class="inline-flex items-center gap-2">
              <svg
                class="w-4 h-4 text-blue-500"
                fill="none"
                stroke="currentColor"
                stroke-width="1.7"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                />
              </svg>
              Phnom Penh, Cambodia
            </span>
            <a
              href="mailto:kimsrenghai@gmail.com"
              class="inline-flex items-center gap-2 hover:text-blue-600 dark:hover:text-blue-400"
            >
              <svg
                class="w-4 h-4 text-blue-500"
                fill="none"
                stroke="currentColor"
                stroke-width="1.7"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                />
              </svg>
              kimsrenghai@gmail.com
            </a>
            <a
              href="https://www.linkedin.com/in/hai-kim-sreng-a0527b274/"
              target="_blank"
              rel="noopener"
              class="inline-flex items-center gap-2 hover:text-blue-600 dark:hover:text-blue-400"
            >
              <svg class="w-4 h-4 text-blue-500" fill="currentColor" viewBox="0 0 24 24">
                <path
                  d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
                />
              </svg>
              LinkedIn
            </a>
          </div>
        </div>

        <!-- Portrait -->
        <div class="relative mx-auto w-full max-w-md">
          <div class="pulse-ring"></div>
          <div class="pulse-ring" style="animation-delay: 1.5s"></div>
          <div class="pulse-ring" style="animation-delay: 3s"></div>
          <span class="orbit-dot" style="--r: 190px; animation: orbit-a 13s linear infinite"></span>
          <span
            class="orbit-dot small"
            style="--r: 215px; animation: orbit-b 18s linear infinite reverse"
          ></span>

          <div
            class="relative mx-auto w-[280px] h-[280px] sm:w-[340px] sm:h-[340px] rounded-full p-1.5 bg-gradient-to-br from-blue-400 via-blue-600 to-blue-800 shadow-2xl z-10"
          >
            <img
              :src="profileImage"
              alt="HAI KIMSRENG"
              class="w-full h-full rounded-full object-cover object-top border-4 border-white dark:border-gray-900"
            />
          </div>

          <!-- Khmer flower accents -->
          <img
            v-for="(pos, i) in flowerPositions"
            :key="i"
            src="../assets/images/flower.png"
            alt=""
            class="khmer-flower absolute w-12 h-12 sm:w-14 sm:h-14 object-contain brightness-75 drop-shadow-lg z-20"
            :class="pos.class"
            :style="{ '--rotation': pos.rotation, 'animation-delay': pos.delay }"
          />

          <!-- Floating stats -->
          <div
            class="absolute left-1/2 -translate-x-1/2 -bottom-8 z-30 w-[min(360px,90vw)] flex justify-center gap-6 px-6 py-4 rounded-2xl border shadow-2xl bg-white border-gray-200 dark:bg-gray-900/95 dark:border-gray-700 float-stats"
          >
            <div v-for="stat in heroStats" :key="stat.label" class="text-center">
              <div class="text-xl sm:text-2xl font-bold text-blue-600 dark:text-blue-400">
                {{ stat.value }}
              </div>
              <div class="mt-1 text-[11px] leading-tight text-gray-500 dark:text-gray-400">
                {{ stat.label }}
              </div>
            </div>
          </div>

          <!-- Industry chips -->
          <div
            v-for="(chip, i) in heroChips"
            :key="chip.label"
            class="hidden xl:flex absolute z-30 flex-col items-center gap-2 w-[104px] py-3 px-2 rounded-2xl border shadow-xl text-center bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-700 chip-float"
            :class="chip.class"
            :style="{ animationDelay: i * 0.4 + 's' }"
          >
            <svg
              class="w-5 h-5 text-blue-500"
              fill="none"
              stroke="currentColor"
              stroke-width="1.7"
              viewBox="0 0 24 24"
            >
              <path stroke-linecap="round" stroke-linejoin="round" :d="chip.icon" />
            </svg>
            <span class="text-[11px] font-semibold leading-tight">{{ chip.label }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- About -->
    <section
      id="about"
      class="py-20 sm:py-24 bg-gray-50 dark:bg-gray-900 border-y border-gray-200 dark:border-gray-800"
    >
      <div class="container mx-auto px-5 sm:px-7 grid lg:grid-cols-2 gap-12 items-start">
        <div class="reveal">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-blue-600 dark:text-blue-400"
          >
            About
          </p>
          <h2 class="mt-3 text-3xl sm:text-4xl font-bold tracking-tight">
            Leading people, building systems
          </h2>
          <p class="mt-5 text-gray-600 dark:text-gray-300 leading-relaxed">
            I am a motivated Full-Stack and Mobile Developer who now leads a team at DRDC. I work
            with Laravel, Next.js, Nest.js, PostgreSQL, Redis and Flutter, and I enjoy designing
            systems, managing the team and keeping our servers running reliably.
          </p>
          <div class="mt-6 flex flex-wrap gap-2">
            <span
              v-for="skill in softSkills"
              :key="skill"
              class="px-4 py-1.5 rounded-full text-sm font-medium bg-blue-100 text-blue-700 dark:bg-blue-900/50 dark:text-blue-300"
            >
              {{ skill }}
            </span>
          </div>
        </div>

        <div class="reveal grid gap-5">
          <!-- Current work -->
          <div
            class="p-6 rounded-2xl border-l-4 border-blue-500 bg-white border border-gray-200 dark:bg-gray-950 dark:border-gray-800 shadow-lg"
          >
            <div class="flex items-center justify-between gap-3">
              <div
                class="text-xs font-semibold uppercase tracking-wider text-blue-600 dark:text-blue-400"
              >
                Current Work
              </div>
              <span
                class="inline-flex items-center gap-1.5 px-2.5 py-0.5 rounded-full text-[11px] font-semibold uppercase tracking-wider bg-blue-100 text-blue-700 dark:bg-blue-900/40 dark:text-blue-300"
              >
                <span class="w-1.5 h-1.5 rounded-full bg-blue-500 animate-pulse"></span>
                Present
              </span>
            </div>
            <h3 class="mt-2 text-lg font-bold">{{ currentWork.role }}</h3>
            <p class="text-sm text-gray-500 dark:text-gray-400">
              {{ currentWork.org }} · {{ currentWork.location }}
            </p>
            <p class="mt-3 text-sm text-gray-600 dark:text-gray-300">{{ currentWork.summary }}</p>
            <div class="mt-4 flex flex-wrap gap-2">
              <span
                v-for="tag in currentWork.tags"
                :key="tag"
                class="px-2.5 py-1 rounded-md text-xs bg-gray-100 text-gray-700 dark:bg-gray-800 dark:text-gray-300"
              >
                {{ tag }}
              </span>
            </div>
          </div>

          <!-- Certification -->
          <div
            class="p-6 rounded-2xl border bg-white border-gray-200 dark:bg-gray-950 dark:border-gray-800 shadow-lg"
          >
            <div
              class="text-xs font-semibold uppercase tracking-wider text-blue-600 dark:text-blue-400"
            >
              Certification
            </div>
            <h3 class="mt-2 font-bold">AWS Cloud Computing – Certificate of Completion</h3>
            <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">
              Online learning in system design, cloud fundamentals, and backend architecture.
            </p>
          </div>

          <!-- Languages -->
          <div
            class="p-6 rounded-2xl border bg-white border-gray-200 dark:bg-gray-950 dark:border-gray-800 shadow-lg"
          >
            <div
              class="text-xs font-semibold uppercase tracking-wider text-blue-600 dark:text-blue-400"
            >
              Languages
            </div>
            <div class="mt-4 space-y-4">
              <div v-for="lang in languages" :key="lang.name">
                <div class="flex justify-between text-sm font-semibold">
                  <span>{{ lang.name }}</span>
                  <span class="text-gray-500 dark:text-gray-400">{{ lang.level }}</span>
                </div>
                <div class="mt-1.5 h-1.5 rounded-full bg-gray-200 dark:bg-gray-800 overflow-hidden">
                  <div
                    class="h-full rounded-full bg-gradient-to-r from-blue-500 to-blue-600 transition-all duration-700"
                    :style="{ width: lang.percent + '%' }"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience -->
    <section id="experience" class="relative py-20 sm:py-24 overflow-hidden">
      <div class="container mx-auto px-5 sm:px-7 grid lg:grid-cols-[1fr_0.9fr] gap-14 items-start">
        <div class="reveal">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-blue-600 dark:text-blue-400"
          >
            Career
          </p>
          <h2 class="mt-3 text-3xl sm:text-4xl font-bold tracking-tight">
            Where I've Made <span class="text-blue-600 dark:text-blue-400">Impact</span>
          </h2>
          <p class="mt-5 text-gray-600 dark:text-gray-300">
            Leading the team on drone and automation projects, and keeping the systems behind them
            running.
          </p>

          <div class="relative mt-10 pl-16">
            <div
              class="absolute left-[23px] top-4 bottom-4 w-0.5 bg-blue-200 dark:bg-blue-900"
            ></div>
            <div
              v-for="item in experience"
              :key="item.role"
              class="reveal relative pb-10 last:pb-0"
            >
              <div
                class="absolute -left-16 top-0 w-12 h-12 rounded-full flex items-center justify-center border shadow-lg"
                :class="
                  item.current
                    ? 'bg-gradient-to-br from-blue-500 to-blue-700 border-transparent text-white'
                    : 'bg-white border-gray-200 text-blue-500 dark:bg-gray-900 dark:border-gray-700'
                "
              >
                <svg
                  class="w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1.7"
                  viewBox="0 0 24 24"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" :d="item.icon" />
                </svg>
              </div>

              <div
                class="p-6 rounded-2xl border bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-800 shadow-md"
              >
                <div class="flex flex-wrap items-center gap-3">
                  <h3 class="text-lg font-bold">{{ item.role }}</h3>
                  <span
                    v-if="item.current"
                    class="inline-flex items-center gap-1.5 px-2.5 py-0.5 rounded-full text-[11px] font-semibold uppercase tracking-wider bg-blue-100 text-blue-700 dark:bg-blue-900/40 dark:text-blue-300"
                  >
                    <span class="w-1.5 h-1.5 rounded-full bg-blue-500 animate-pulse"></span>
                    Current
                  </span>
                </div>
                <div class="mt-1 font-semibold text-blue-600 dark:text-blue-400">
                  {{ item.org }}
                </div>
                <div class="text-sm text-gray-500 dark:text-gray-400">{{ item.period }}</div>
                <ul class="mt-4 space-y-2">
                  <li
                    v-for="bullet in item.bullets"
                    :key="bullet"
                    class="flex gap-2 text-sm text-gray-600 dark:text-gray-300"
                  >
                    <span class="text-blue-500 font-bold">›</span>
                    <span>{{ bullet }}</span>
                  </li>
                </ul>
                <div v-if="item.tags" class="mt-5 flex flex-wrap gap-2">
                  <span
                    v-for="tag in item.tags"
                    :key="tag"
                    class="px-2.5 py-1 rounded-md text-xs font-medium bg-blue-50 text-blue-700 dark:bg-blue-900/30 dark:text-blue-300"
                  >
                    {{ tag }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="reveal relative">
          <div class="relative aspect-square max-w-md mx-auto">
            <div
              class="absolute inset-0 rounded-full border border-blue-500/20 animate-spin-slow"
            ></div>
            <div
              class="absolute inset-[7%] rounded-full border border-blue-500/15 animate-spin-slow-reverse"
            ></div>

            <!-- Photo -->
            <div
              class="absolute inset-[14%] rounded-full p-1.5 bg-gradient-to-br from-blue-400 via-blue-600 to-blue-800 shadow-2xl"
            >
              <div
                class="relative w-full h-full rounded-full overflow-hidden border-4 border-white dark:border-gray-900"
              >
                <img
                  :src="experienceImage"
                  alt="Software engineer at DRDC"
                  class="w-full h-full object-cover"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-blue-950/50 via-transparent to-transparent"
                ></div>
                <img
                  src="../assets/images/kh_flower.png"
                  alt=""
                  class="absolute inset-0 w-full h-full object-cover opacity-10 mix-blend-overlay"
                />
              </div>
            </div>

            <!-- Floating badges -->
            <div
              class="chip-float absolute left-0 top-[16%] z-10 flex items-center gap-2 px-4 py-2.5 rounded-xl border shadow-xl bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-700"
            >
              <span class="w-2 h-2 rounded-full bg-blue-500 animate-pulse"></span>
              <span class="text-xs font-semibold">Software Engineer</span>
            </div>
            <div
              class="chip-float absolute right-0 bottom-[14%] z-10 flex items-center gap-2 px-4 py-2.5 rounded-xl border shadow-xl bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-700"
              style="animation-delay: 0.8s"
            >
              <span class="text-xs font-semibold">Servers · Docker · Proxmox</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Workflow -->
    <section
      id="workflow"
      class="py-20 sm:py-24 bg-blue-50/60 dark:bg-gray-900 border-y border-gray-200 dark:border-gray-800"
    >
      <div class="container mx-auto px-5 sm:px-7">
        <div class="reveal max-w-2xl mx-auto text-center">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-blue-600 dark:text-blue-400"
          >
            Workflow
          </p>
          <h2 class="mt-3 text-3xl sm:text-4xl font-bold tracking-tight">How I Lead a Project</h2>
          <p class="mt-4 text-gray-600 dark:text-gray-300">
            From understanding the problem to delivering it, I guide the team at every stage. Hover
            or click any step to explore it.
          </p>
        </div>

        <div class="reveal mt-14">
          <div class="relative">
            <div
              class="hidden md:block absolute left-[6%] right-[6%] top-7 h-0.5 bg-blue-200 dark:bg-gray-700"
            >
              <div
                class="h-full rounded-full bg-gradient-to-r from-blue-500 to-blue-300 transition-all duration-700"
                :style="{ width: railWidth }"
              ></div>
            </div>

            <div class="relative grid grid-cols-2 md:grid-cols-6 gap-6">
              <button
                v-for="(step, i) in workflowSteps"
                :key="step.name"
                @click="selectStep(i)"
                @mouseenter="selectStep(i)"
                class="flex flex-col items-center gap-3 text-center group"
              >
                <span
                  class="w-14 h-14 rounded-full flex items-center justify-center border transition-all duration-500"
                  :class="
                    i <= workflowIndex
                      ? 'bg-gradient-to-br from-blue-500 to-blue-700 border-transparent text-white shadow-xl'
                      : 'bg-white border-gray-300 text-gray-400 dark:bg-gray-800 dark:border-gray-700'
                  "
                  :style="i === workflowIndex ? { transform: 'scale(1.12)' } : {}"
                >
                  <svg
                    class="w-6 h-6"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="1.7"
                    viewBox="0 0 24 24"
                  >
                    <path stroke-linecap="round" stroke-linejoin="round" :d="step.icon" />
                  </svg>
                </span>
                <span class="text-xs font-mono text-blue-600 dark:text-blue-400">{{
                  step.num
                }}</span>
                <span
                  class="text-sm font-semibold leading-tight"
                  :class="
                    i === workflowIndex
                      ? 'text-gray-900 dark:text-white'
                      : 'text-gray-500 dark:text-gray-400'
                  "
                >
                  {{ step.name }}
                </span>
              </button>
            </div>
          </div>

          <div class="mt-12 max-w-2xl mx-auto min-h-[64px] text-center">
            <div
              class="text-xs font-semibold uppercase tracking-widest text-blue-600 dark:text-blue-400"
            >
              Stage {{ workflowSteps[workflowIndex].num }} · {{ workflowSteps[workflowIndex].name }}
            </div>
            <p class="mt-2 text-gray-700 dark:text-gray-300">
              {{ workflowSteps[workflowIndex].description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects -->
    <section id="projects" class="py-20 sm:py-24">
      <div class="container mx-auto px-5 sm:px-7">
        <div class="reveal max-w-2xl mx-auto text-center">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-blue-600 dark:text-blue-400"
          >
            Projects
          </p>
          <h2 class="mt-3 text-3xl sm:text-4xl font-bold tracking-tight">
            Work at DRDC &amp; Beyond
          </h2>
          <p class="mt-4 text-gray-600 dark:text-gray-300">
            Drone delivery, automation and platform projects.
          </p>
        </div>

        <div class="reveal mt-14 grid lg:grid-cols-2 gap-12 items-center">
          <div
            class="relative aspect-[16/10] rounded-2xl overflow-hidden shadow-2xl bg-gradient-to-br from-blue-500 via-blue-700 to-blue-950 flex items-center justify-center"
          >
            <img
              v-if="currentProjectImage"
              :src="currentProjectImage"
              :alt="currentProject.name"
              class="absolute inset-0 w-full h-full object-cover"
            />
            <template v-else>
              <img
                src="../assets/images/kh_flower.png"
                alt=""
                class="absolute inset-0 w-full h-full object-cover opacity-25 mix-blend-overlay"
              />
              <span class="relative text-[120px] font-bold text-white/90 leading-none">{{
                projectNumber
              }}</span>
            </template>
            <span
              v-if="currentProjectImage"
              class="absolute top-4 left-4 px-3 py-1 rounded-full bg-black/50 backdrop-blur text-white text-xs font-mono"
            >
              {{ projectNumber }}
            </span>
          </div>

          <div>
            <div class="flex items-center gap-3">
              <span class="text-sm font-mono text-blue-600 dark:text-blue-400">{{
                projectNumber
              }}</span>
              <span class="h-px w-7 bg-gray-300 dark:bg-gray-700"></span>
              <span class="text-xs uppercase tracking-widest text-gray-500 dark:text-gray-400">{{
                currentProject.category
              }}</span>
            </div>
            <h3 class="mt-4 text-3xl font-bold">❖ {{ currentProject.name }}</h3>
            <p class="mt-4 text-gray-600 dark:text-gray-300 leading-relaxed">
              {{ currentProject.description }}
            </p>
            <ul class="mt-4 space-y-2">
              <li
                v-for="point in currentProject.highlights"
                :key="point"
                class="flex gap-2 text-sm text-gray-600 dark:text-gray-300"
              >
                <span class="text-blue-500 font-bold">›</span>
                <span>{{ point }}</span>
              </li>
            </ul>
            <div class="mt-5 flex flex-wrap gap-2">
              <span
                v-for="tag in currentProject.tags"
                :key="tag"
                class="px-3 py-1 rounded-lg text-xs font-medium border bg-gray-50 border-gray-200 text-blue-700 dark:bg-gray-800 dark:border-gray-700 dark:text-blue-300"
              >
                {{ tag }}
              </span>
            </div>

            <div class="mt-10 flex items-center justify-between">
              <div class="flex gap-2">
                <button
                  v-for="(project, i) in projects"
                  :key="project.name"
                  @click="activeProject = i"
                  class="h-2 rounded-full transition-all duration-300"
                  :class="
                    i === activeProject ? 'w-7 bg-blue-600' : 'w-2 bg-gray-300 dark:bg-gray-700'
                  "
                  :aria-label="'Show ' + project.name"
                ></button>
              </div>
              <div class="flex gap-3">
                <button
                  @click="prevProject"
                  class="w-10 h-10 rounded-full border flex items-center justify-center bg-white border-gray-300 hover:bg-blue-600 hover:border-blue-600 hover:text-white dark:bg-gray-900 dark:border-gray-700 transition-all duration-300"
                  aria-label="Previous project"
                >
                  <svg
                    class="w-4 h-4 rotate-180"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M5 12h14m-6-6l6 6-6 6"
                    />
                  </svg>
                </button>
                <button
                  @click="nextProject"
                  class="w-10 h-10 rounded-full border flex items-center justify-center bg-white border-gray-300 hover:bg-blue-600 hover:border-blue-600 hover:text-white dark:bg-gray-900 dark:border-gray-700 transition-all duration-300"
                  aria-label="Next project"
                >
                  <svg
                    class="w-4 h-4"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M5 12h14m-6-6l6 6-6 6"
                    />
                  </svg>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills -->
    <section
      id="skills"
      class="py-20 sm:py-24 bg-gray-50 dark:bg-gray-900 border-y border-gray-200 dark:border-gray-800"
    >
      <div class="container mx-auto px-5 sm:px-7">
        <div class="reveal max-w-2xl mx-auto text-center">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-blue-600 dark:text-blue-400"
          >
            Capabilities
          </p>
          <h2 class="mt-3 text-3xl sm:text-4xl font-bold tracking-tight">What I Do Best</h2>
          <p class="mt-4 text-gray-600 dark:text-gray-300">
            Team leadership, server management and full-stack development, brought together to
            deliver working systems.
          </p>
        </div>

        <div class="reveal mt-14 grid sm:grid-cols-2 lg:grid-cols-4 gap-6">
          <div
            v-for="cap in capabilities"
            :key="cap.title"
            class="group p-6 rounded-2xl border bg-white border-gray-200 hover:border-blue-400 hover:shadow-2xl hover:-translate-y-1.5 dark:bg-gray-950 dark:border-gray-800 dark:hover:border-blue-500 transition-all duration-300"
          >
            <div
              class="w-12 h-12 rounded-xl flex items-center justify-center mb-5 bg-blue-100 text-blue-600 group-hover:bg-blue-600 group-hover:text-white dark:bg-blue-900/40 dark:text-blue-400 transition-colors duration-300"
            >
              <svg
                class="w-6 h-6"
                fill="none"
                stroke="currentColor"
                stroke-width="1.7"
                viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" :d="cap.icon" />
              </svg>
            </div>
            <h3 class="font-bold mb-3">{{ cap.title }}</h3>
            <ul class="space-y-2">
              <li
                v-for="item in cap.items"
                :key="item"
                class="flex gap-2 text-sm text-gray-600 dark:text-gray-400"
              >
                <span class="text-blue-500 font-bold">›</span>
                {{ item }}
              </li>
            </ul>
          </div>
        </div>

        <!-- Tech Stack -->
        <div
          class="reveal mt-10 p-6 sm:p-8 rounded-2xl border bg-white border-gray-200 dark:bg-gray-950 dark:border-gray-800 shadow-lg flex flex-col lg:flex-row gap-10"
        >
          <div class="lg:w-56 lg:pr-10 lg:border-r border-gray-200 dark:border-gray-800">
            <div class="text-4xl font-bold text-blue-600 dark:text-blue-400">{{ techCount }}+</div>
            <div class="mt-2 text-sm text-gray-500 dark:text-gray-400">
              Technologies I work with
            </div>
          </div>
          <div class="flex-1 grid sm:grid-cols-2 gap-6">
            <div v-for="group in techGroups" :key="group.name">
              <div
                class="text-xs font-semibold uppercase tracking-wider text-gray-500 dark:text-gray-400"
              >
                {{ group.name }}
              </div>
              <div class="mt-3 flex flex-wrap gap-2">
                <span
                  v-for="tech in group.items"
                  :key="tech"
                  class="px-3 py-1.5 rounded-lg text-sm border bg-gray-50 border-gray-200 hover:bg-blue-600 hover:border-blue-600 hover:text-white dark:bg-gray-800 dark:border-gray-700 transition-all duration-300"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact -->
    <section id="contact" class="py-20 sm:py-24">
      <div class="container mx-auto px-5 sm:px-7">
        <div class="reveal max-w-2xl mx-auto text-center">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-blue-600 dark:text-blue-400"
          >
            Contact
          </p>
          <h2 class="mt-3 text-3xl sm:text-4xl font-bold tracking-tight">Get In Touch</h2>
          <p class="mt-4 text-gray-600 dark:text-gray-300">
            I'm open to new opportunities, interesting projects, or a chat about technology.
          </p>
        </div>

        <div class="mt-12 grid lg:grid-cols-[1.1fr_0.9fr] gap-6 lg:gap-8 items-stretch">
          <!-- Contact cards -->
          <div class="reveal grid sm:grid-cols-2 gap-4">
            <a
              v-for="item in contacts"
              :key="item.label"
              :href="item.href"
              :target="item.external ? '_blank' : undefined"
              :rel="item.external ? 'noopener' : undefined"
              class="group flex items-center gap-4 p-5 rounded-2xl border bg-gray-50 border-gray-200 hover:border-blue-400 hover:-translate-y-0.5 hover:shadow-lg dark:bg-gray-900 dark:border-gray-800 dark:hover:border-blue-500 transition-all duration-300"
              :class="item.wide ? 'sm:col-span-2' : ''"
            >
              <span
                class="w-11 h-11 shrink-0 rounded-xl flex items-center justify-center bg-blue-100 text-blue-600 group-hover:bg-blue-600 group-hover:text-white dark:bg-blue-900/40 dark:text-blue-400 transition-colors duration-300"
              >
                <svg
                  class="w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1.7"
                  viewBox="0 0 24 24"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" :d="item.icon" />
                </svg>
              </span>
              <span class="min-w-0 flex-1">
                <span
                  class="block text-[11px] uppercase tracking-wider text-gray-500 dark:text-gray-400"
                  >{{ item.label }}</span
                >
                <span class="block font-semibold truncate">{{ item.value }}</span>
              </span>
              <svg
                class="w-4 h-4 shrink-0 text-gray-400 group-hover:text-blue-500 transition-colors duration-300"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M7 17L17 7M7 7h10v10" />
              </svg>
            </a>
          </div>

          <!-- Call to action -->
          <div
            class="reveal relative overflow-hidden rounded-3xl p-8 sm:p-10 shadow-2xl bg-gradient-to-br from-blue-600 via-blue-700 to-blue-950 text-white flex flex-col justify-between gap-10"
          >
            <img
              src="../assets/images/kbach_kh.png"
              alt=""
              class="absolute -bottom-6 -right-6 w-48 opacity-10 object-contain pointer-events-none"
            />
            <div class="relative">
              <span
                class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full bg-white/10 border border-white/20 text-xs font-semibold"
              >
                <span class="relative flex h-2 w-2">
                  <span
                    class="absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75 animate-ping"
                  ></span>
                  <span class="relative inline-flex h-2 w-2 rounded-full bg-emerald-400"></span>
                </span>
                Available for opportunities
              </span>
              <h3 class="mt-6 text-2xl sm:text-3xl font-bold leading-tight">
                Let's build something together
              </h3>
              <p class="mt-3 text-blue-100/90">
                Whether it's a drone delivery system, an automation project or a new idea, I'd love
                to hear from you.
              </p>
            </div>
            <div class="relative flex flex-col sm:flex-row gap-3">
              <a
                href="mailto:kimsrenghai@gmail.com"
                class="inline-flex h-12 flex-1 justify-center items-center rounded-xl border border-white bg-white px-6 text-blue-700 font-semibold hover:-translate-y-0.5 hover:shadow-xl transition-all duration-300"
              >
                Email Me
              </a>
              <button
                @click="saveContact"
                class="inline-flex h-12 flex-1 justify-center items-center gap-2 rounded-xl border border-white/40 px-6 font-semibold hover:bg-white/10 hover:-translate-y-0.5 transition-all duration-300"
              >
                Save Contact
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="py-8 border-t border-gray-200 dark:border-gray-800 bg-white dark:bg-gray-950">
      <div
        class="container mx-auto px-5 sm:px-7 flex flex-col md:flex-row items-center justify-between gap-5"
      >
        <div class="flex items-center gap-4">
          <img src="../assets/images/logo_darkBlue.png" alt="DRDC" class="h-8 w-auto dark:hidden" />
          <img
            src="../assets/images/logo_white.png"
            alt="DRDC"
            class="hidden h-8 w-auto dark:block"
          />
          <span class="font-bold text-lg">
            <span class="text-blue-600 dark:text-blue-400">HAI</span> KIMSRENG
          </span>
        </div>
        <p class="text-sm text-gray-500 dark:text-gray-400">
          &copy; 2026 HAI KIMSRENG. All rights reserved.
        </p>
        <div class="flex gap-3">
          <a
            href="https://www.linkedin.com/in/hai-kim-sreng-a0527b274/"
            target="_blank"
            rel="noopener"
            class="p-2.5 rounded-full bg-gray-100 text-gray-600 hover:bg-blue-600 hover:text-white dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-blue-600 dark:hover:text-white hover:scale-110 transition-all duration-300"
            aria-label="LinkedIn Profile"
          >
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
              />
            </svg>
          </a>
          <a
            href="https://github.com/Kimsreng28"
            target="_blank"
            rel="noopener"
            class="p-2.5 rounded-full bg-gray-100 text-gray-600 hover:bg-blue-600 hover:text-white dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-blue-600 dark:hover:text-white hover:scale-110 transition-all duration-300"
            aria-label="GitHub Profile"
          >
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
              />
            </svg>
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import profileImage from '../assets/images/Kimsreng.jpg'
import flowerBanner from '../assets/images/flower_banner.jpg'

// Optional photo for the "Impact" circle. Add src/assets/images/experience.jpg
// (or .png / .webp) and it is picked up automatically. Until then the flower
// banner is shown, so the build never fails on a missing file.
const customExperience = import.meta.glob('../assets/images/experience.{jpg,jpeg,png,webp}', {
  eager: true,
  import: 'default',
})
const experienceImage = Object.values(customExperience)[0] || flowerBanner

// Optional project screenshots. Add files to src/assets/images/projects/ named
// after the project slug, e.g. gcs-drone-delivery.jpg, drdt.png, bytefarm.webp.
const projectImages = import.meta.glob('../assets/images/projects/*.{jpg,jpeg,png,webp}', {
  eager: true,
  import: 'default',
})

const ICONS = {
  team: 'M16 21v-2a4 4 0 00-4-4H6a4 4 0 00-4 4v2M9 11a4 4 0 100-8 4 4 0 000 8zM22 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75',
  server: 'M2 5h20v5H2zM2 14h20v5H2zM6 7.5h.01M6 16.5h.01',
  drone:
    'M12 12m-2 0a2 2 0 104 0 2 2 0 10-4 0M4 4l4 4M20 4l-4 4M4 20l4-4M20 20l-4-4M7 7a7 7 0 000 10M17 7a7 7 0 010 10',
  code: 'M16 18l6-6-6-6M8 6l-6 6 6 6',
  factory: 'M2 20V8l6 4V8l6 4V4h8v16z',
  search: 'M21 21l-4.35-4.35M11 18a7 7 0 100-14 7 7 0 000 14z',
  calendar:
    'M8 2v4M16 2v4M3 10h18M5 4h14a2 2 0 012 2v14a2 2 0 01-2 2H5a2 2 0 01-2-2V6a2 2 0 012-2z',
  check: 'M22 11.08V12a10 10 0 11-5.93-9.14M22 4L12 14.01l-3-3',
  location:
    'M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0zM15 11a3 3 0 11-6 0 3 3 0 016 0z',
  mail: 'M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z',
  phone:
    'M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z',
  linkedin:
    'M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-4 0v7h-4v-7a6 6 0 016-6zM2 9h4v12H2zM4 2a2 2 0 110 4 2 2 0 010-4z',
  github:
    'M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22',
}

export default {
  name: 'HomeView',
  data() {
    return {
      darkMode: true,
      profileImage: profileImage,
      experienceImage: experienceImage,
      mobileMenuOpen: false,
      isScrolled: false,
      scrollProgress: 0,
      workflowIndex: 0,
      workflowTimer: null,
      activeProject: 0,
      observer: null,
      navItems: [
        { id: 'home', name: 'Home' },
        { id: 'about', name: 'About' },
        { id: 'experience', name: 'Experience' },
        { id: 'workflow', name: 'Workflow' },
        { id: 'projects', name: 'Projects' },
        { id: 'skills', name: 'Skills' },
        { id: 'contact', name: 'Contact' },
      ],
      heroStats: [
        { value: '5', label: 'Projects' },
        { value: '2+', label: 'Years Experience' },
        { value: '5+', label: 'Technologies' },
      ],
      flowerPositions: [
        { class: '-top-4 -left-4', rotation: '-12deg', delay: '0s' },
        { class: '-top-4 -right-4', rotation: '12deg', delay: '0.5s' },
        { class: 'top-[45%] -left-6', rotation: '12deg', delay: '1s' },
        { class: 'top-[45%] -right-6', rotation: '-12deg', delay: '1.5s' },
      ],
      heroChips: [
        { label: 'Drone Delivery', icon: ICONS.drone, class: 'top-0 left-0' },
        { label: 'Industrial Automation', icon: ICONS.factory, class: 'top-4 right-0' },
        { label: 'Server Management', icon: ICONS.server, class: 'top-[45%] -left-10' },
        { label: 'Full-Stack Development', icon: ICONS.code, class: 'top-[45%] -right-10' },
      ],
      experience: [
        {
          role: 'Team Lead, Full Stack Developer',
          org: 'DRDC',
          period: 'Present',
          current: true,
          icon: ICONS.team,
          bullets: [
            'Lead the development team: plan work, assign tasks, review code and unblock developers.',
            'Architect and build services for DRDT (DroneOps AI), a drone delivery and surveillance platform based on microservices.',
            'Lead GCS Drone Delivery, the ground control station for drone delivery operations.',
            'Manage the team’s servers: Proxmox virtual machines, Docker deployments, backups and monitoring.',
            'Built a server-monitor dashboard and Telegram alerts so problems are seen before users report them.',
            'Deploy and publish apps with Docker, Coolify and Cloudflare Tunnel.',
            'Built ByteFarm, a hosting sales website with customer portal, invoices, support tickets and card, bank and KHQR payments.',
            'Run the Factory I/O server used for industrial automation simulation.',
          ],
          tags: [
            'Server Management',
            'Microservices',
            'Docker',
            'Proxmox',
            'PostgreSQL',
            'Redis',
            'Cloudflare Tunnel',
          ],
        },
        {
          role: 'Backend Developer',
          org: 'EasyEazy Application · Team / Real-World Project',
          period: '2026 – Present',
          current: false,
          icon: ICONS.server,
          bullets: [
            'Built the EasyEazy application backend using a professional software architecture.',
            'Designed and developed a complete management platform with authentication, admin dashboards and role-based permissions.',
            'Integrated Facebook, Google and native authentication.',
            'Developed an FCM notification system for real-time alerts.',
            'Added multiple vendors, each with their own KHQR payment, plus shipping and delivery methods.',
          ],
          tags: ['Vendure', 'Nest.js', 'PostgreSQL', 'TypeScript', 'OAuth', 'FCM', 'Facebook', 'KHQR'],
        },
        {
          role: 'Full-Stack Developer',
          org: 'E-Management Platform · Personal / Academic Project',
          period: '2025 – 2026',
          current: false,
          icon: ICONS.code,
          bullets: [
            'Built a full modern E-Management Platform from scratch using a professional software architecture.',
            'Designed and developed a complete management platform with authentication, admin dashboards and role-based permissions.',
            'Integrated Redis for caching and performance optimization.',
            'Developed a Telegram Bot notification system for real-time alerts.',
            'Added multiple payment methods including Stripe, KHQR Bakong and Cash on Delivery.',
            'Implemented a chat system for text, image, voice and calls between users.',
          ],
          tags: [
            'Laravel',
            'Next.js',
            'PostgreSQL',
            'Redis',
            'OAuth2',
            'Telegram Bot API',
            'Stripe',
            'KHQR Bakong',
          ],
        },
        {
          role: 'Project Developer',
          org: 'Real-Time Quiz App (DICE) · Team / Academic Project',
          period: '2024',
          current: false,
          icon: ICONS.team,
          bullets: [
            'Developed a real-time quiz platform where many students join at the same time.',
            'Built the web version with Vue.js and the mobile version with Flutter.',
            'Implemented socket communication for real-time synchronization.',
          ],
          tags: ['Vue.js', 'Nest.js', 'Socket.IO', 'Flutter'],
        },
        {
          role: 'Project Developer, E-Commerce',
          org: 'E-Commerce Platform · Team / Academic Project',
          period: '2024',
          current: false,
          icon: ICONS.code,
          bullets: [
            'Developed an e-commerce platform for browsing products and checking out with multiple payment methods.',
            'Implemented multi-role access (Admin, Vendor, Customer).',
            'Integrated a microservice for file storage using Go.',
            'Designed a responsive UI with Next.js for multiple devices.',
          ],
          tags: ['Next.js', 'Nest.js', 'MySQL', 'Go', 'OAuth'],
        },
        {
          role: 'Bachelor of Engineering in ICT',
          org: 'Institute of Technology of Cambodia (ITC)',
          period: '2021 – Present',
          current: false,
          icon: ICONS.calendar,
          bullets: [
            'Coursework in data structures, networking, databases, system administration and cloud computing.',
            'Completed an AWS Cloud Computing certificate covering system design, cloud fundamentals and backend architecture.',
          ],
          tags: ['Networking', 'Databases', 'Cloud Computing'],
        },
      ],
      workflowSteps: [
        {
          num: '01',
          name: 'Understand the Problem',
          icon: ICONS.search,
          description:
            'Clarify what the team needs to deliver and why, before any code is written.',
        },
        {
          num: '02',
          name: 'Plan the Work',
          icon: ICONS.calendar,
          description: 'Break each project into tasks, priorities and milestones for the team.',
        },
        {
          num: '03',
          name: 'Lead the Team',
          icon: ICONS.team,
          description: 'Assign tasks, guide the developers and keep communication clear.',
        },
        {
          num: '04',
          name: 'Build & Integrate',
          icon: ICONS.code,
          description: 'Develop GCS Drone Delivery and other systems together with the team.',
        },
        {
          num: '05',
          name: 'Manage Servers',
          icon: ICONS.server,
          description: 'Set up, monitor and maintain the servers the projects run on.',
        },
        {
          num: '06',
          name: 'Deliver & Review',
          icon: ICONS.check,
          description: 'Review results, fix issues and deliver the finished work.',
        },
      ],
      projects: [
        {
          slug: 'gcs-drone-delivery',
          name: 'GCS Drone Delivery',
          category: 'DRDC Project',
          description:
            'A ground control station for drone delivery operations. Operators plan missions, watch drones in flight and manage deliveries from one dashboard. I lead the team that builds it.',
          highlights: [
            'Mission planning and live drone monitoring',
            'Built and led by the DRDC team',
            'Runs on servers we manage ourselves',
          ],
          tags: ['Drone Delivery', 'Ground Control Station'],
        },
        {
          slug: 'drdt',
          name: 'DRDT (DroneOps AI)',
          category: 'DRDC Project',
          description:
            'A drone delivery and surveillance platform split into independent microservices, so each part can be developed, deployed and scaled on its own.',
          highlights: [
            'Microservices architecture',
            'Delivery and surveillance in one platform',
            'Deployed and monitored on our own infrastructure',
          ],
          tags: ['Microservices', 'Drone Delivery', 'Surveillance', 'Docker'],
        },
        {
          slug: 'drdc',
          name: 'DRDC',
          category: 'DRDC Project',
          description:
            'Core DRDC project work, led by our team from planning through delivery and server deployment.',
          highlights: ['Delivered from planning to release', 'Servers managed by the same team'],
          tags: ['Project Delivery', 'Server Deployment'],
        },
        {
          slug: 'factory-io',
          name: 'Factory I/O',
          category: 'Other Project',
          description:
            'An industrial automation simulation for factory scenarios, hosted on our own server and reachable securely through a Cloudflare tunnel.',
          highlights: [
            'Self-hosted on our own server',
            'Secure remote access without opening ports',
            'Used for automation practice and testing',
          ],
          tags: ['Industrial Automation', 'Simulation', 'Cloudflare Tunnel'],
        },
        {
          slug: 'bytefarm',
          name: 'ByteFarm',
          category: 'Other Project',
          description:
            'A web hosting company website with a customer portal. Customers order VPS, hosting and colocation, pay by card, bank transfer or KHQR, and open support tickets. Admins manage plans, orders and invoices.',
          highlights: [
            'Customer dashboard, invoices and tickets',
            'Stripe, bank transfer and KHQR payments',
            'Admin panel, status page and blog',
          ],
          tags: ['Next.js', 'PostgreSQL', 'Redis', 'Docker', 'Coolify'],
        },
      ],
      capabilities: [
        {
          title: 'Team Leadership',
          icon: ICONS.team,
          items: ['Manage and lead the team', 'Teamwork & communication', 'Problem-solving'],
        },
        {
          title: 'Server Management',
          icon: ICONS.server,
          items: ['Server management', 'Docker & Redis', 'CI/CD'],
        },
        {
          title: 'Drone Delivery',
          icon: ICONS.drone,
          items: ['GCS Drone Delivery', 'DRDT & DRDC projects'],
        },
        {
          title: 'Full-Stack Development',
          icon: ICONS.code,
          items: ['Laravel & Nest.js', 'Next.js & Vue.js', 'Flutter mobile'],
        },
      ],
      techGroups: [
        { name: 'Backend', items: ['Laravel', 'NestJS', 'Node.js', 'Go'] },
        { name: 'Frontend', items: ['Next.js', 'Vue.js', 'React', 'TypeScript', 'Tailwind'] },
        { name: 'Mobile', items: ['Flutter'] },
        { name: 'Data & DevOps', items: ['PostgreSQL', 'MySQL', 'Redis', 'Docker', 'Socket.IO'] },
      ],
      currentWork: {
        role: 'Full Stack Developer',
        org: 'DRDC',
        location: 'Phnom Penh, Cambodia',
        summary:
          'Building GCS Drone Delivery and DRDT, and managing the servers these systems run on.',
        tags: ['GCS Drone Delivery', 'DRDT', 'DRDC', 'Server Management', 'Docker'],
      },
      languages: [
        { name: 'Khmer', level: 'Native', percent: 100 },
        { name: 'English', level: 'Fluent', percent: 75 },
        { name: 'French', level: 'Basic', percent: 35 },
      ],
      softSkills: [
        'Communication',
        'Teamwork',
        'Leadership',
        'Problem-Solving',
        'Time Management',
        'Adaptability',
      ],
      contacts: [
        {
          label: 'Email',
          value: 'kimsrenghai@gmail.com',
          href: 'mailto:kimsrenghai@gmail.com',
          icon: ICONS.mail,
          wide: true,
        },
        { label: 'Phone', value: '069-376-706', href: 'tel:069376706', icon: ICONS.phone },
        {
          label: 'Location',
          value: 'Phnom Penh, Cambodia',
          href: 'https://maps.google.com/?q=Phnom+Penh',
          external: true,
          icon: ICONS.location,
        },
        {
          label: 'LinkedIn',
          value: 'hai-kim-sreng',
          href: 'https://www.linkedin.com/in/hai-kim-sreng-a0527b274/',
          external: true,
          icon: ICONS.linkedin,
        },
        {
          label: 'GitHub',
          value: 'Kimsreng28',
          href: 'https://github.com/Kimsreng28',
          external: true,
          icon: ICONS.github,
        },
      ],
    }
  },
  computed: {
    currentProject() {
      return this.projects[this.activeProject]
    },
    currentProjectImage() {
      const slug = this.currentProject.slug
      const match = Object.keys(projectImages).find((path) =>
        new RegExp('/' + slug + '\\.[a-z]+$', 'i').test(path),
      )
      return match ? projectImages[match] : null
    },
    projectNumber() {
      return String(this.activeProject + 1).padStart(2, '0')
    },
    railWidth() {
      return (this.workflowIndex / (this.workflowSteps.length - 1)) * 100 + '%'
    },
    techCount() {
      return this.techGroups.reduce((total, group) => total + group.items.length, 0)
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
      this.mobileMenuOpen = false
      const element = document.getElementById(sectionId)
      if (element) {
        window.scrollTo({
          top: element.offsetTop - 80,
          behavior: 'smooth',
        })
      }
    },
    handleScroll() {
      const scrollTop = window.pageYOffset || document.documentElement.scrollTop
      const maxScroll = document.documentElement.scrollHeight - window.innerHeight
      this.isScrolled = scrollTop > 50
      this.scrollProgress = maxScroll > 0 ? scrollTop / maxScroll : 0
    },
    selectStep(index) {
      this.workflowIndex = index
      clearInterval(this.workflowTimer)
    },
    prevProject() {
      const total = this.projects.length
      this.activeProject = (this.activeProject - 1 + total) % total
    },
    nextProject() {
      this.activeProject = (this.activeProject + 1) % this.projects.length
    },
    saveContact() {
      const vcard = [
        'BEGIN:VCARD',
        'VERSION:3.0',
        'N:;HAI KIMSRENG;;;',
        'FN:HAI KIMSRENG',
        'ORG:DRDC',
        'TITLE:Full Stack Developer',
        'TEL;TYPE=CELL:069-376-706',
        'EMAIL:kimsrenghai@gmail.com',
        'ADR;TYPE=WORK:;;Phnom Penh;;;;Cambodia',
        'URL:https://github.com/Kimsreng28',
        'END:VCARD',
      ].join('\r\n')

      const url = URL.createObjectURL(new Blob([vcard], { type: 'text/vcard' }))
      const link = document.createElement('a')
      link.href = url
      link.download = 'HAI_KIMSRENG.vcf'
      link.click()
      URL.revokeObjectURL(url)
    },
  },
  mounted() {
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
      this.darkMode = true
      document.documentElement.classList.add('dark')
    } else {
      this.darkMode = false
      document.documentElement.classList.remove('dark')
    }

    window.addEventListener('scroll', this.handleScroll)
    this.handleScroll()

    this.observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('in')
            this.observer.unobserve(entry.target)
          }
        })
      },
      { threshold: 0.15 },
    )
    document.querySelectorAll('.reveal').forEach((el) => this.observer.observe(el))

    this.workflowTimer = setInterval(() => {
      this.workflowIndex = (this.workflowIndex + 1) % this.workflowSteps.length
    }, 3500)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
    clearInterval(this.workflowTimer)
    if (this.observer) this.observer.disconnect()
  },
}
</script>

<style>
.reveal {
  opacity: 0;
  transform: translateY(26px);
  transition:
    opacity 0.8s ease,
    transform 0.8s ease;
}

.reveal.in {
  opacity: 1;
  transform: none;
}

.rise {
  opacity: 0;
  animation: rise 0.9s cubic-bezier(0.22, 0.61, 0.36, 1) forwards;
}

@keyframes rise {
  to {
    opacity: 1;
    transform: none;
  }
  from {
    opacity: 0;
    transform: translateY(26px);
  }
}

.pulse-ring {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 200px;
  height: 200px;
  margin: -100px 0 0 -100px;
  border: 1.5px solid rgba(59, 130, 246, 0.3);
  border-radius: 50%;
  opacity: 0;
  pointer-events: none;
  z-index: 0;
  animation: pulse-ring-anim 4.5s ease infinite;
}

@keyframes pulse-ring-anim {
  0% {
    opacity: 0.55;
    transform: scale(0.55);
  }
  70% {
    opacity: 0.12;
  }
  100% {
    opacity: 0;
    transform: scale(1.5);
  }
}

.orbit-dot {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #60a5fa;
  box-shadow: 0 0 9px rgba(96, 165, 250, 0.6);
  transform-origin: 0 0;
  pointer-events: none;
  z-index: 1;
}

.orbit-dot.small {
  width: 5px;
  height: 5px;
  opacity: 0.75;
}

@keyframes orbit-a {
  from {
    transform: rotate(0) translate(var(--r));
  }
  to {
    transform: rotate(1turn) translate(var(--r));
  }
}

@keyframes orbit-b {
  from {
    transform: rotate(90deg) translate(var(--r));
  }
  to {
    transform: rotate(450deg) translate(var(--r));
  }
}

@keyframes float-stats {
  0%,
  100% {
    transform: translate(-50%, 0);
  }
  50% {
    transform: translate(-50%, -12px);
  }
}

.float-stats {
  animation: float-stats 8s ease-in-out infinite;
}

@keyframes chip-float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-12px);
  }
}

.chip-float {
  animation: chip-float 7s ease-in-out infinite;
}

.khmer-flower {
  animation: flower-float 3s ease-in-out infinite;
}

@keyframes flower-float {
  0%,
  100% {
    transform: translateY(0) rotate(var(--rotation));
  }
  50% {
    transform: translateY(-5px) rotate(var(--rotation));
  }
}

.animate-spin-slow {
  animation: spin-slow 26s linear infinite;
}

.animate-spin-slow-reverse {
  animation: spin-slow 19s linear infinite reverse;
}

@keyframes spin-slow {
  to {
    transform: rotate(1turn);
  }
}

@media (prefers-reduced-motion: reduce) {
  .reveal,
  .rise {
    opacity: 1 !important;
    transform: none !important;
    animation: none !important;
    transition: none !important;
  }

  .orbit-dot,
  .pulse-ring,
  .float-stats,
  .chip-float,
  .khmer-flower {
    animation: none !important;
  }
}

html {
  scroll-behavior: smooth;
}
</style>