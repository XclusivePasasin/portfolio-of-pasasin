<template>
  <div class="min-h-screen bg-background text-foreground relative">
    <!-- Navigation dots -->
    <nav class="fixed left-8 top-1/2 -translate-y-1/2 z-10 block">
      <div class="flex flex-col gap-4">
        <button
          v-for="section in sections"
          :key="section"
          @click="scrollToSection(section)"
          :class="[
            'w-3 h-3 rounded-full transition-all duration-300',
            activeSection === section ? 'bg-foreground scale-125' : 'bg-muted-foreground/30 hover:bg-muted-foreground/60'
          ]"
          :aria-label="`Navigate to ${section}`"
        />
      </div>
    </nav>

    <main class="max-w-7xl mx-auto px-6 sm:px-8 lg:px-16">
      <!-- Header / Intro Section -->
      <header id="intro" ref="introRef" class="min-h-screen flex items-center">
        <div class="grid lg:grid-cols-5 gap-12 sm:gap-16 w-full">
          <div class="lg:col-span-3 space-y-6 sm:space-y-8">
            <div class="space-y-3 sm:space-y-2">
              <div class="text-sm text-muted-foreground font-mono tracking-wider">PORTFOLIO / 2025</div>
              <h1 class="text-5xl sm:text-6xl lg:text-7xl font-light tracking-tight">
                Antonio
                <br />
                <span class="text-muted-foreground">Pasasin</span>
              </h1>
            </div>

            <div class="space-y-6 max-w-md">
              <p class="text-lg sm:text-xl text-muted-foreground leading-relaxed">
                Tech Leader crafting intelligent systems at the intersection of 
                <span class="text-foreground">software development</span>, 
                <span class="text-foreground">automation</span>, 
                and 
                <span class="text-foreground">innovation</span>.
              </p>
              <div class="flex flex-col sm:flex-row sm:items-center gap-3 sm:gap-4 text-sm text-muted-foreground">
                <div class="flex items-center gap-2">
                  <div class="w-2 h-2 bg-red-500 rounded-full animate-pulse"></div>
                  Available for work
                </div>
                <div>El Salvador - San Salvador</div>
              </div>
            </div>
          </div>

          <div class="lg:col-span-2 flex flex-col justify-end space-y-6 sm:space-y-8 mt-8 lg:mt-0">
            <div class="space-y-4">
              <div class="text-sm text-muted-foreground font-mono">CURRENTLY</div>
              <div class="space-y-2">
                <div class="text-foreground">Technical leader</div>
                <div class="text-xs text-muted-foreground">2025 — Present</div>
              </div>
            </div>

            <div class="space-y-4">
              <div class="text-sm text-muted-foreground font-mono">FOCUS</div>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="skill in skills"
                  :key="skill"
                  class="px-3 py-1 text-xs border border-border rounded-full hover:border-muted-foreground/50 transition-colors duration-300"
                >
                  {{ skill }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Work Section -->
      <section id="work" ref="workRef" class="min-h-screen py-20 sm:py-32">
        <div class="space-y-12 sm:space-y-16">
          <div class="flex flex-col sm:flex-row sm:items-end sm:justify-between gap-4">
            <h2 class="text-3xl sm:text-4xl font-light">Selected Work</h2>
            <div class="text-sm text-muted-foreground font-mono">2019 — 2025</div>
          </div>

          <div class="space-y-8 sm:space-y-12">
            <div
              v-for="(job, index) in jobs"
              :key="index"
              class="group grid lg:grid-cols-12 gap-4 sm:gap-8 py-6 sm:py-8 border-b border-border/50 hover:border-border transition-colors duration-500"
            >
              <div class="lg:col-span-2">
                <div class="text-xl sm:text-2xl font-light text-muted-foreground group-hover:text-foreground transition-colors duration-500">
                  {{ job.year }}
                </div>
              </div>

              <div class="lg:col-span-6 space-y-3">
                <div>
                  <h3 class="text-lg sm:text-xl font-medium">{{ job.role }}</h3>
                  <div class="text-muted-foreground">{{ job.company }}</div>
                </div>
                <p class="text-muted-foreground leading-relaxed max-w-lg">{{ job.description }}</p>
              </div>

              <div class="lg:col-span-4 flex flex-wrap gap-2 lg:justify-end mt-2 lg:mt-0">
                <span
                  v-for="tech in job.tech"
                  :key="tech"
                  :class="['px-2 py-1 text-xs rounded transition-all duration-500', `neon-text-${tech.toLowerCase().replace(/[\.\s]/g, '-')}`, 'group-hover:text-foreground']"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Education Section -->
      <section id="thoughts" ref="thoughtsRef" class="min-h-screen py-20 sm:py-32">
        <div class="space-y-12 sm:space-y-16">
          <h2 class="text-3xl sm:text-4xl font-light">Academic Information</h2>

          <div class="grid gap-6 sm:gap-8 lg:grid-cols-2">
            <article
              v-for="(post, index) in posts"
              :key="index"
              class="group relative overflow-hidden border border-border rounded-lg transition-all duration-500 cursor-pointer
                    hover:border-muted-foreground/50 hover:shadow-lg focus-within:shadow-lg"
              tabindex="0"
              aria-label="Academic card"
            >
              <!-- Contenedor con alto fijo: NO cambia el layout del grid -->
              <div class="relative h-44 sm:h-48 p-6 sm:p-8">
                <!-- Siempre visible: SOLO el título -->
                <h3
                  class="text-lg sm:text-xl font-medium line-clamp-2
                        transition-colors duration-300
                        group-hover:text-muted-foreground group-focus-within:text-muted-foreground"
                >
                  {{ post.title }}
                </h3>

                <!-- Capa de detalle (absoluta) con FADE que no altera el alto -->
                <div
                  class="pointer-events-none absolute inset-0 p-6 sm:p-8 flex flex-col justify-end
                        opacity-0 translate-y-2
                        transition-all duration-500 ease-out
                        group-hover:opacity-100 group-hover:translate-y-0
                        group-focus-within:opacity-100 group-focus-within:translate-y-0"
                >
                  <!-- Gradiente para efecto faded -->
                  <div class="absolute inset-x-0 bottom-0 h-24 bg-gradient-to-t from-background/95 via-background/70 to-transparent"></div>

                  <!-- Contenido (queda sobre el gradiente) -->
                  <div class="relative space-y-2">
                    <div class="flex items-center gap-2 text-xs">
                      <span
                        class="inline-flex items-center rounded-full border px-2 py-0.5 font-mono uppercase tracking-wide
                              text-muted-foreground border-muted-foreground/30"
                      >
                        {{ post.kind }}
                      </span>
                      <span class="text-muted-foreground">•</span>
                      <span class="text-muted-foreground">{{ post.period }}</span>
                    </div>

                    <p class="text-sm sm:text-base leading-relaxed">
                      {{ post.institution }}
                    </p>
                  </div>
                </div>
              </div>
            </article>
          </div>
        </div>
      </section>


      <!-- Connect Section -->
      <section id="connect" ref="connectRef" class="py-20 sm:py-32">
        <div class="grid lg:grid-cols-2 gap-12 sm:gap-16">
          <div class="space-y-6 sm:space-y-8">
            <h2 class="text-3xl sm:text-4xl font-light">Let's Connect</h2>

            <div class="space-y-6">
              <p class="text-lg sm:text-xl text-muted-foreground leading-relaxed">
                Always interested in new opportunities, collaborations, and conversations about technology and design.
              </p>

              <div class="space-y-4">
                <a
                  href="mailto:test@example.com"
                  class="group flex items-center gap-3 text-foreground hover:text-muted-foreground transition-colors duration-300"
                >
                  <span class="text-base sm:text-lg">eliazar.rebollo23@gmail.com</span>
                  <svg
                    class="w-5 h-5 transform group-hover:translate-x-1 transition-transform duration-300"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                  </svg>
                </a>
              </div>
            </div>
          </div>

          <div class="space-y-6 sm:space-y-8">
            <div class="text-sm text-muted-foreground font-mono">ELSEWHERE</div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <a
                v-for="social in socials"
                :key="social.name"
                :href="social.url"
                class="group p-4 border border-border rounded-lg hover:border-muted-foreground/50 transition-all duration-300 hover:shadow-sm"
              >
                <div class="space-y-2">
                  <div class="text-foreground group-hover:text-muted-foreground transition-colors duration-300">
                    {{ social.name }}
                  </div>
                  <div class="text-sm text-muted-foreground">{{ social.handle }}</div>
                </div>
              </a>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer -->
      <footer class="py-12 sm:py-16 border-t border-border">
        <div class="flex flex-col lg:flex-row justify-between items-start lg:items-center gap-6 sm:gap-8">
          <div class="space-y-2">
            <div class="text-sm text-muted-foreground">© 2025 Antonio Pasasin. All rights reserved.</div>
          </div>

          <div class="flex items-center gap-4">
            <button
              @click="toggleTheme"
              class="group p-3 rounded-lg border border-border hover:border-muted-foreground/50 transition-all duration-300"
              aria-label="Toggle theme"
            >
              <svg
                v-if="isDark"
                class="w-4 h-4 text-muted-foreground group-hover:text-foreground transition-colors duration-300"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
                  clip-rule="evenodd"
                />
              </svg>
              <svg
                v-else
                class="w-4 h-4 text-muted-foreground group-hover:text-foreground transition-colors duration-300"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
              </svg>
            </button>

            <!-- <button class="group p-3 rounded-lg border border-border hover:border-muted-foreground/50 transition-all duration-300">
              <svg
                class="w-4 h-4 text-muted-foreground group-hover:text-foreground transition-colors duration-300"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"
                />
              </svg>
            </button> -->
          </div>
        </div>
      </footer>
    </main>

    <div class="fixed bottom-0 left-0 right-0 h-24 bg-gradient-to-t from-background via-background/80 to-transparent pointer-events-none"></div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

const isDark = ref(true)
const activeSection = ref('intro')
const sections = ['intro', 'work', 'thoughts', 'connect']

const introRef = ref(null)
const workRef = ref(null)
const thoughtsRef = ref(null)
const connectRef = ref(null)

const skills = ['Odoo', 'Python', 'Laravel', 'Vue', 'Docker', 'Tailwind CSS', 'SQL', 'Google Cloud', 'Linux', 'Automation']

const jobs = [
  {
    year: 'Junio 2025 - Present',
    role: 'Technical leader',
    company: 'Velatek S.A De C.V',
    description: 'As a technical leader at Velatek, an official Odoo partner, I lead the implementation and development of customized Odoo solutions to optimize business processes. I develop custom modules, automate workflows, and provide specialized technical support to various companies, ensuring efficient integrations and an optimized user experience. My focus is on creating scalable solutions and continuously improving systems to meet specific client needs.',
    tech: ['Odoo', 'Leadership', 'Automation', 'Technical support', 'PostgreSQL', 'Google Cloud', 'Linux', 'Python', 'XML']
  },
  {
    year: 'Junio 2024 - Present',
    role: 'FullStack Developer',
    company: 'Clobi Technologies S.A De C.V',
    description: 'I developed and maintained web applications for various clients, optimizing internal processes. I led the development of microservices with Flask, created dynamic applications with Vue.js and Laravel, and automated processes to improve efficiency. I implemented deployments with Docker, designed normalized relational database schemas, performed quality testing, and prototyped interfaces in Figma to collaborate on system design. I worked with agile methodologies (Scrum and Kanban) to deliver comprehensive solutions, focusing on usability and workflow optimization.',
    tech: ['React', 'Python', 'Docker', 'Scrum', 'Vue.js', 'Laravel', 'Figma', 'SQL']
  },
  {
    year: 'April 2023 - December 2024',
    role: 'Frontend Developer and Analyst Freelance',
    company: 'ITCA - FEPADE',
    description: 'As part of the ITCA-FEPADE Innovation 2024 project, I led the front-end development of generative artificial intelligence tools. My contributions included generating ideas and analytical approaches to solve technical and functional problems, optimizing the user experience and tool efficiency.',
    tech: ['Python', 'Vue', 'Critical Thinking']
  },
  {
    year: 'July 2022 - November 2022',
    role: 'Database administrator',
    company: 'Citylab S.A De C.V',
    description: 'I specialized in SQL Server, honing expertise in database management and query optimization. I significantly improved the performance of complex, slow-running queries by leveraging execution plan analysis and implementing effective indexing strategies. Additionally, I adeptly managed large datasets to ensure seamless support for daily operations.',
    tech: ['SQL Server', 'Teamwork', 'Report Builder']
  }
]

const posts = [
    {
      kind: 'education',
      institution: 'ITCA Fepade | Escuela Especializada en Ingeniería',
      title: 'Software Development Engineering Technician',
      period: '2023–2024'
    },
    {
      kind: 'education',
      institution: 'Cisco Networking Academy',
      title: 'NDG Linux',
      period: '2022'
    },
    {
      kind: 'education',
      institution: 'Instituto Nacional Técnico Industrial',
      title: 'Software Development Technician',
      period: '2020–2022'
    },
    {
      kind: 'certification',
      institution: 'ITCA Fepade',
      title: 'CCNAv7: Introduction to Networks',
      period: '2023'
    },
    {
      kind: 'certification',
      institution: 'IBM',
      title: 'Docker Essentials',
      period: '2023'
    },
    {
      kind: 'certification',
      institution: 'Udemy',
      title: 'Git y GitHub',
      period: '2023'
    }
]

const socials = [
  { name: 'GitHub', handle: '@XclusivePasasin', url: 'https://github.com/XclusivePasasin' },
  { name: 'Instagram', handle: '@Pasasin.py', url: 'https://www.instagram.com/pasasin.py?igsh=OXIwaWszMHk3anh3' },
  { name: 'LinkedIn', handle: 'Antonio Pasasin', url: 'www.linkedin.com/in/antonio-pasasin' }
]



const toggleTheme = () => {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
}

const scrollToSection = (section) => {
  const element = document.getElementById(section)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth', block: 'start' })
    activeSection.value = section
  }
}

const updateActiveSection = () => {
  const scrollPosition = window.scrollY + window.innerHeight / 2
  let currentSection = 'intro'

  for (const section of sections) {
    const element = document.getElementById(section)
    if (element) {
      const offsetTop = element.offsetTop
      const offsetHeight = element.offsetHeight
      if (scrollPosition >= offsetTop && scrollPosition < offsetTop + offsetHeight) {
        currentSection = section
        break
      }
    }
  }
  activeSection.value = currentSection
}

let observer = null
let scrollHandler = null

onMounted(async () => {
  document.documentElement.classList.toggle('dark', isDark.value)
  await nextTick()

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.remove('opacity-0')
          entry.target.classList.add('animate-fade-in-up')
        }
      })
    },
    { threshold: 0.1, rootMargin: '0px 0px -10% 0px' }
  )

  const sectionRefs = [introRef.value, workRef.value, thoughtsRef.value, connectRef.value]
  sectionRefs.forEach((section) => {
    if (section) {
      section.classList.add('opacity-0')
      observer.observe(section)
    }
  })

  scrollHandler = () => {
    updateActiveSection()
  }
  window.addEventListener('scroll', scrollHandler)
  updateActiveSection()
})

onUnmounted(() => {
  if (observer) observer.disconnect()
  if (scrollHandler) window.removeEventListener('scroll', scrollHandler)
})
</script>

<style scoped>

.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>