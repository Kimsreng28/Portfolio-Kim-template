<template>
  <div id="app" class="bg-gray-900 text-white">
    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 bg-gray-900/90 backdrop-blur-sm py-4 px-6 shadow-lg">
      <div class="container mx-auto flex justify-between items-center">
        <div class="text-2xl font-bold"><span class="text-blue-500">HAI</span> KIMSRENG</div>
        <div class="hidden md:flex space-x-8">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="'#' + item.id"
            @click.prevent="scrollTo(item.id)"
            class="hover:text-blue-500 transition-all duration-300"
          >
            {{ item.name }}
          </a>
        </div>
        <div class="md:hidden">
          <button @click="mobileMenuOpen = !mobileMenuOpen" class="text-white focus:outline-none">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                v-if="!mobileMenuOpen"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              ></path>
              <path
                v-else
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              ></path>
            </svg>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div v-if="mobileMenuOpen" class="md:hidden bg-gray-800 mt-4 py-4 px-6 rounded-lg shadow-xl">
        <div class="flex flex-col space-y-4">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="'#' + item.id"
            @click.prevent="scrollToAndCloseMenu(item.id)"
            class="hover:text-blue-500 transition-all duration-300 py-2"
          >
            {{ item.name }}
          </a>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex items-center pt-16 relative overflow-hidden">
      <!-- Background Effects -->
      <div class="absolute inset-0 z-0">
        <div
          class="absolute top-1/4 left-1/4 w-64 h-64 bg-blue-500 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-pulse"
        ></div>
        <div
          class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-blue-700 rounded-full mix-blend-multiply filter blur-3xl opacity-10 animate-pulse delay-1000"
        ></div>
        <div
          class="absolute top-3/4 left-1/2 w-80 h-80 bg-blue-400 rounded-full mix-blend-multiply filter blur-3xl opacity-15 animate-pulse delay-500"
        ></div>
      </div>

      <div class="container mx-auto px-6 py-20 relative z-10">
        <div class="flex flex-col lg:flex-row items-center justify-between gap-12">
          <!-- Left Content -->
          <div ref="leftContent" class="lg:w-1/2">
            <div class="mb-8">
              <div class="inline-block bg-blue-600/20 px-4 py-2 rounded-full mb-6">
                <span class="text-blue-400 text-sm font-semibold">🚀 FULL-STACK DEVELOPER</span>
              </div>
              <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold mb-4 leading-tight">
                <span
                  class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600"
                >
                  HAI KIMSRENG
                </span>
              </h1>
              <h2 class="text-2xl md:text-3xl text-gray-300 mb-6">
                <span class="text-blue-300">Software Engineer</span> &
                <span class="text-blue-200">Mobile Developer</span>
              </h2>
              <p class="text-lg text-gray-300 mb-8 max-w-2xl">
                Crafting digital experiences with cutting-edge technologies. Specialized in building
                scalable web applications, real-time systems, and cross-platform mobile solutions
                that solve real-world problems.
              </p>
            </div>

            <!-- Quick Stats -->
            <div class="grid grid-cols-2 md:grid-cols-3 gap-4 mb-8">
              <div class="bg-gray-800/50 backdrop-blur-sm p-4 rounded-xl border border-gray-700">
                <div class="text-blue-400 font-bold text-2xl">10+</div>
                <div class="text-sm text-gray-300">Projects</div>
              </div>
              <div class="bg-gray-800/50 backdrop-blur-sm p-4 rounded-xl border border-gray-700">
                <div class="text-blue-400 font-bold text-2xl">2+</div>
                <div class="text-sm text-gray-300">Years Experience</div>
              </div>
              <div class="bg-gray-800/50 backdrop-blur-sm p-4 rounded-xl border border-gray-700">
                <div class="text-blue-400 font-bold text-2xl">5+</div>
                <div class="text-sm text-gray-300">Technologies</div>
              </div>
            </div>

            <!-- Tech Stack -->
            <div class="mb-8">
              <h3 class="text-lg font-semibold text-gray-300 mb-4">Tech Stack</h3>
              <div class="flex flex-wrap gap-3">
                <div
                  v-for="tech in mainTech"
                  :key="tech"
                  class="bg-gray-800/70 hover:bg-blue-900/30 px-4 py-2 rounded-lg border border-gray-700 hover:border-blue-500 transition-all duration-300 group cursor-pointer"
                >
                  <span class="text-gray-300 group-hover:text-blue-300 transition-colors">
                    {{ tech }}
                  </span>
                </div>
              </div>
            </div>

            <!-- CTA Buttons -->
            <div class="flex flex-wrap gap-4">
              <button
                @click="scrollTo('contact')"
                class="bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 px-6 py-3 rounded-lg font-semibold transition-all duration-300 flex items-center shadow-lg hover:shadow-xl"
              >
                <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                  />
                </svg>
                Get In Touch
              </button>
              <a
                href="https://github.com/Kimsreng28"
                target="_blank"
                class="bg-gray-800/70 hover:bg-gray-700/70 px-6 py-3 rounded-lg font-semibold transition-all duration-300 flex items-center border border-gray-700 hover:border-gray-600"
              >
                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
                  <path
                    d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                  />
                </svg>
                View GitHub
              </a>
              <button
                @click="scrollTo('projects')"
                class="bg-gray-800/30 hover:bg-gray-700/50 px-6 py-3 rounded-lg font-semibold transition-all duration-300 flex items-center border border-gray-700/50 hover:border-gray-600/70"
              >
                <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"
                  />
                </svg>
                View Projects
              </button>
            </div>
          </div>

          <!-- Right Content - Profile Image & Info -->
          <div ref="rightContent" class="lg:w-1/2 flex justify-center">
            <div class="relative">
              <!-- Main Profile Card -->
              <div class="relative z-20">
                <!-- Profile Image Container -->
                <div class="relative w-64 h-64 md:w-80 md:h-80 lg:w-96 lg:h-96 mx-auto">
                  <!-- Outer Glow Ring -->
                  <div
                    class="absolute inset-0 bg-gradient-to-r from-blue-500 to-blue-700 rounded-full animate-spin-slow"
                    style="animation-duration: 8s"
                  ></div>

                  <!-- Profile Image Background -->
                  <div
                    class="absolute inset-2 bg-gradient-to-br from-blue-900 via-gray-900 to-blue-950 rounded-full flex items-center justify-center"
                  >
                    <!-- Profile Image Placeholder -->
                    <div class="relative w-full h-full rounded-full overflow-hidden">
                      <!-- Fallback Initials -->
                      <div
                        v-if="!profileImageLoaded"
                        class="w-full h-full flex items-center justify-center bg-gradient-to-br from-blue-800 to-blue-900"
                      >
                        <div class="text-center">
                          <div
                            class="text-7xl md:text-8xl lg:text-9xl font-bold text-white opacity-80"
                          >
                            HK
                          </div>
                          <div class="mt-4 text-blue-200 text-lg md:text-xl">Developer</div>
                        </div>
                      </div>

                      <!-- Actual Profile Image -->
                      <img
                        src="../assets/images/Kimsreng.jpg"
                        alt="Profile Kim"
                        class="w-full h-full object-cover"
                      />
                    </div>
                  </div>

                  <!-- Floating Tech Badges -->
                  <div
                    class="absolute -top-4 -right-4 bg-blue-600 text-white px-4 py-2 rounded-lg shadow-lg transform rotate-6 z-30"
                  >
                    <div class="text-sm font-bold">Laravel</div>
                  </div>
                  <div
                    class="absolute -bottom-4 -left-4 bg-blue-500 text-white px-4 py-2 rounded-lg shadow-lg transform -rotate-6 z-30"
                  >
                    <div class="text-sm font-bold">Flutter</div>
                  </div>
                  <div
                    class="absolute top-1/2 -right-8 bg-blue-700 text-white px-4 py-2 rounded-lg shadow-lg z-30"
                  >
                    <div class="text-sm font-bold">Next.js</div>
                  </div>
                  <div
                    class="absolute top-1/2 -left-8 bg-blue-800 text-white px-4 py-2 rounded-lg shadow-lg z-30"
                  >
                    <div class="text-sm font-bold">Vue.js</div>
                  </div>
                </div>

                <!-- Info Card Below Image -->
                <div
                  class="mt-8 bg-gray-800/80 backdrop-blur-sm rounded-2xl p-6 border border-gray-700/50 shadow-2xl max-w-md mx-auto"
                >
                  <div class="flex items-center justify-between mb-4">
                    <div>
                      <h3 class="text-xl font-bold text-white">HAI KIMSRENG</h3>
                      <p class="text-blue-300">Software Engineer</p>
                    </div>
                    <div
                      class="w-12 h-12 bg-gradient-to-r from-blue-600 to-blue-800 rounded-full flex items-center justify-center"
                    >
                      <svg
                        class="w-6 h-6 text-white"
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

                  <div class="space-y-3">
                    <div class="flex items-center text-gray-300">
                      <svg
                        class="w-5 h-5 mr-3 text-blue-400"
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
                    <div class="flex items-center text-gray-300">
                      <svg
                        class="w-5 h-5 mr-3 text-blue-400"
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
                    <div class="flex items-center text-gray-300">
                      <svg
                        class="w-5 h-5 mr-3 text-blue-400"
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

                  <div class="mt-6 pt-6 border-t border-gray-700/50">
                    <div class="flex justify-center space-x-4">
                      <button
                        @click="scrollTo('contact')"
                        class="text-blue-400 hover:text-blue-300 transition-colors"
                      >
                        Contact Me
                      </button>
                      <span class="text-gray-600">•</span>
                      <button
                        @click="scrollTo('projects')"
                        class="text-blue-400 hover:text-blue-300 transition-colors"
                      >
                        View Work
                      </button>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Background Decorative Elements -->
              <div
                class="absolute -top-8 -right-8 w-40 h-40 bg-blue-500 rounded-full blur-3xl opacity-20 z-0"
              ></div>
              <div
                class="absolute -bottom-8 -left-8 w-60 h-60 bg-blue-700 rounded-full blur-3xl opacity-15 z-0"
              ></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Scroll Indicator -->
      <div ref="scrollIndicator" class="absolute bottom-8 left-1/2 transform -translate-x-1/2">
        <button
          @click="scrollTo('about')"
          class="flex flex-col items-center text-gray-400 hover:text-blue-400 transition-colors"
        >
          <span class="text-sm mb-2">Explore More</span>
          <svg class="w-6 h-6 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
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

    <!-- About Section -->
    <section id="about" class="py-20 bg-gray-800">
      <div class="container mx-auto px-6">
        <h2 ref="aboutTitle" class="text-3xl font-bold mb-12 text-center">About Me</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
          <div ref="aboutLeft" class="opacity-0">
            <p class="text-gray-300 text-lg mb-6">
              I am a motivated Full-Stack Developer and Mobile Developer with experience building
              web applications, real-time systems, and modern user interfaces. I work with Laravel,
              Next.js, Nest.js, PostgreSQL, Redis, and also develop mobile apps using Flutter.
            </p>
            <p class="text-gray-300 text-lg mb-6">
              I enjoy solving problems, designing systems, and creating efficient platforms such as
              e-management and e-commerce systems. I am passionate about learning new skills,
              working with teams, and delivering good-quality work.
            </p>
            <div class="flex items-center space-x-4 mb-6">
              <div class="bg-gray-700 p-3 rounded-lg">
                <div class="text-blue-400 font-bold">2+</div>
                <div class="text-sm">Years Experience</div>
              </div>
              <div class="bg-gray-700 p-3 rounded-lg">
                <div class="text-blue-400 font-bold">10+</div>
                <div class="text-sm">Projects Completed</div>
              </div>
              <div class="bg-gray-700 p-3 rounded-lg">
                <div class="text-blue-400 font-bold">5+</div>
                <div class="text-sm">Technologies</div>
              </div>
            </div>
          </div>
          <div ref="aboutRight" class="opacity-0">
            <h3 class="text-xl font-bold mb-4">Core Competencies</h3>
            <div class="grid grid-cols-2 gap-4">
              <div
                v-for="skill in coreCompetencies"
                :key="skill.name"
                class="bg-gray-900 p-4 rounded-lg"
              >
                <div class="font-semibold text-blue-400">{{ skill.name }}</div>
                <div class="text-sm text-gray-400 mt-1">{{ skill.items.join(', ') }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="py-20">
      <div class="container mx-auto px-6">
        <h2 ref="experienceTitle" class="text-3xl font-bold mb-12 text-center opacity-0">
          Work Experience
        </h2>
        <div class="space-y-12">
          <div
            v-for="(exp, index) in experiences"
            :key="index"
            :ref="`exp-${index}`"
            class="opacity-0"
          >
            <div class="bg-gray-800 rounded-xl p-6 shadow-lg">
              <div class="flex flex-col md:flex-row justify-between mb-4">
                <h3 class="text-xl font-bold text-blue-400">{{ exp.title }}</h3>
                <div class="text-gray-400">{{ exp.period }}</div>
              </div>
              <p class="text-gray-300 mb-6">{{ exp.description }}</p>
              <div class="flex flex-wrap gap-2 mb-4">
                <span
                  v-for="tech in exp.technologies"
                  :key="tech"
                  class="bg-blue-900/50 text-blue-300 px-3 py-1 rounded-full text-sm"
                >
                  {{ tech }}
                </span>
              </div>
              <ul class="text-gray-300 space-y-2">
                <li
                  v-for="(detail, detailIndex) in exp.details"
                  :key="detailIndex"
                  class="flex items-start"
                >
                  <div class="text-blue-500 mr-2">•</div>
                  <div>{{ detail }}</div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="py-20 bg-gray-800">
      <div class="container mx-auto px-6">
        <h2 ref="projectsTitle" class="text-3xl font-bold mb-12 text-center opacity-0">
          Key Projects
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="project in projects"
            :key="project.id"
            :ref="`project-${project.id}`"
            class="opacity-0 bg-gray-900 rounded-xl overflow-hidden shadow-lg hover:shadow-2xl transition-all duration-300"
          >
            <div class="p-6">
              <div class="text-blue-400 font-bold text-xl mb-2">{{ project.name }}</div>
              <div class="text-gray-400 text-sm mb-4">{{ project.year }}</div>
              <p class="text-gray-300 mb-6">{{ project.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tech in project.technologies"
                  :key="tech"
                  class="bg-gray-800 text-blue-300 px-3 py-1 rounded-full text-xs"
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
    <section id="education" class="py-20">
      <div class="container mx-auto px-6">
        <h2 ref="educationTitle" class="text-3xl font-bold mb-12 text-center opacity-0">
          Education
        </h2>
        <div ref="educationContent" class="bg-gray-800 rounded-xl p-8 shadow-lg opacity-0">
          <h3 class="text-2xl font-bold text-blue-400 mb-2">
            Bachelor of Engineering in Information & Communication Technology (ICT)
          </h3>
          <div class="text-gray-400 text-lg mb-6">
            Institute of Technology of Cambodia (ITC) - 2021 - Present
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <div v-for="year in educationYears" :key="year.year" class="bg-gray-900 p-6 rounded-lg">
              <h4 class="text-xl font-bold mb-4 text-blue-300">{{ year.year }}</h4>
              <ul class="space-y-2">
                <li v-for="(course, index) in year.courses" :key="index" class="text-gray-300">
                  {{ course }}
                </li>
              </ul>
            </div>
          </div>

          <div class="mt-10">
            <h3 class="text-xl font-bold mb-4">Certifications & Professional Development</h3>
            <div class="bg-gray-900 p-6 rounded-lg">
              <div class="text-blue-400 font-bold text-lg mb-2">
                AWS Cloud Computing – Certificate of Completion
              </div>
              <p class="text-gray-300">
                Online learning in system design, cloud fundamentals, and backend architecture.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-20 bg-gray-800">
      <div class="container mx-auto px-6">
        <h2 ref="contactTitle" class="text-3xl font-bold mb-12 text-center opacity-0">Contact</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
          <div ref="contactLeft" class="opacity-0">
            <h3 class="text-2xl font-bold mb-6">Get In Touch</h3>
            <p class="text-gray-300 mb-8">
              I'm always open to discussing new opportunities, interesting projects, or just having
              a chat about technology.
            </p>

            <div class="space-y-6">
              <div class="flex items-center">
                <div class="bg-blue-600 p-3 rounded-lg mr-4">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                    ></path>
                  </svg>
                </div>
                <div>
                  <div class="font-bold">Email</div>
                  <div class="text-gray-300">kimsrenghai@gmail.com</div>
                </div>
              </div>

              <div class="flex items-center">
                <div class="bg-blue-600 p-3 rounded-lg mr-4">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
                    ></path>
                  </svg>
                </div>
                <div>
                  <div class="font-bold">Phone</div>
                  <div class="text-gray-300">069-367-706</div>
                </div>
              </div>

              <div class="flex items-center">
                <div class="bg-blue-600 p-3 rounded-lg mr-4">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
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
                  <div class="font-bold">Location</div>
                  <div class="text-gray-300">Phnom Penh, Cambodia</div>
                </div>
              </div>
            </div>

            <div class="mt-8">
              <h4 class="text-xl font-bold mb-4">Languages</h4>
              <div class="flex flex-wrap gap-4">
                <div
                  v-for="lang in languages"
                  :key="lang.name"
                  class="bg-gray-900 px-4 py-2 rounded-lg"
                >
                  <div class="font-bold">{{ lang.name }}</div>
                  <div class="text-sm text-gray-400">{{ lang.level }}</div>
                </div>
              </div>
            </div>
          </div>

          <div ref="contactRight" class="opacity-0">
            <h3 class="text-2xl font-bold mb-6">Skills & Abilities</h3>

            <div class="mb-8">
              <h4 class="text-xl font-bold mb-4">Technical Skills</h4>
              <div class="grid grid-cols-2 gap-4">
                <div
                  v-for="skill in technicalSkills"
                  :key="skill.name"
                  class="bg-gray-900 p-4 rounded-lg"
                >
                  <div class="font-bold text-blue-400 mb-2">{{ skill.name }}</div>
                  <div class="h-2 bg-gray-700 rounded-full overflow-hidden">
                    <div
                      class="h-full bg-blue-600 rounded-full"
                      :style="{ width: skill.level + '%' }"
                    ></div>
                  </div>
                </div>
              </div>
            </div>

            <div>
              <h4 class="text-xl font-bold mb-4">Soft Skills</h4>
              <div class="flex flex-wrap gap-3">
                <span
                  v-for="skill in softSkills"
                  :key="skill"
                  class="bg-blue-900/50 text-blue-300 px-4 py-2 rounded-full"
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
    <footer class="bg-gray-900 py-8">
      <div class="container mx-auto px-6">
        <div class="flex flex-col md:flex-row justify-between items-center">
          <div class="text-2xl font-bold mb-4 md:mb-0">
            <span class="text-blue-500">HAI</span> KIMSRENG
          </div>
          <div class="text-gray-400 mb-4 md:mb-0">&copy; 2025 Portfolio. All rights reserved.</div>
          <div class="flex space-x-4">
            <a
              href="https://github.com/Kimsreng28"
              target="_blank"
              class="bg-gray-800 hover:bg-gray-700 p-3 rounded-full transition-all duration-300"
            >
              <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
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
      profileImage: profileImage,
      profileImageLoaded: false,
      navItems: [
        { id: 'home', name: 'Home' },
        { id: 'about', name: 'About' },
        { id: 'experience', name: 'Experience' },
        { id: 'projects', name: 'Projects' },
        { id: 'education', name: 'Education' },
        { id: 'contact', name: 'Contact' },
      ],
      mainTech: ['Laravel', 'Next.js', 'Nest.js', 'Flutter', 'PostgreSQL'],
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
  methods: {
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
    initHeroAnimation() {
      // Hero section animations
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

      gsap.fromTo(
        this.$refs.scrollIndicator,
        { opacity: 0 },
        {
          opacity: 1,
          duration: 1,
          delay: 1.5,
        },
      )
    },
    initScrollAnimations() {
      gsap.registerPlugin(ScrollTrigger)

      // Wait for next tick to ensure DOM is rendered
      this.$nextTick(() => {
        // Animate section titles
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

        // Animate content sections
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

        // Animate experience items - CORRECTED
        this.experiences.forEach((_, index) => {
          // In Vue 3, ref in v-for creates an array
          if (this.$refs[`exp-${index}`]) {
            const element = this.$refs[`exp-${index}`][0] // Get first element from array
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

        // Animate project cards - CORRECTED
        this.projects.forEach((project, index) => {
          if (this.$refs[`project-${project.id}`]) {
            const element = this.$refs[`project-${project.id}`][0] // Get first element from array
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

        // Refresh ScrollTrigger after all animations are set up
        setTimeout(() => {
          ScrollTrigger.refresh()
        }, 1000)
      })
    },
  },
  mounted() {
    // Preload the image
    const img = new Image()
    img.src = this.profileImage
    img.onload = () => {
      this.profileImageLoaded = true // Changed from imageLoaded to profileImageLoaded
    }
    img.onerror = () => {
      this.profileImageLoaded = false
      console.error('Failed to preload profile image at:', this.profileImage)
    }

    // Initialize animations
    this.$nextTick(() => {
      this.initHeroAnimation()
      setTimeout(() => {
        this.initScrollAnimations()
      }, 500)
    })

    window.addEventListener('resize', () => {
      ScrollTrigger.refresh()
    })
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

/* Custom styles for smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Ensure proper spacing */
section {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

/* Mobile menu fix */
@media (max-width: 768px) {
  #home {
    padding-top: 80px;
  }
}

/* Profile image container fix */
.relative .absolute.inset-0 {
  z-index: 1;
}

.relative .absolute.inset-2 {
  z-index: 2;
}
</style>
