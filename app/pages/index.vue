<script setup>
const hoveredExp = ref(null);

const titles = [
  "Software Developer",
  "Full Stack Engineer",
  "Product-Focused Engineer",
  "Mentor & Team Lead"
];

const displayText = ref("");
const isDeleting = ref(false);
const wordIndex = ref(0);
const typeSpeed = ref(150);

const handleTyping = () => {
  const currentFullText = titles[wordIndex.value % titles.length];

  if (isDeleting.value) {
    displayText.value = currentFullText.substring(0, displayText.value.length - 1);
    typeSpeed.value = 50;
  } else {
    displayText.value = currentFullText.substring(0, displayText.value.length + 1);
    typeSpeed.value = 150;
  }

  if (!isDeleting.value && displayText.value === currentFullText) {
    isDeleting.value = true;
    typeSpeed.value = 2000;
  } else if (isDeleting.value && displayText.value === "") {
    isDeleting.value = false;
    wordIndex.value++;
    typeSpeed.value = 500;
  }

  setTimeout(handleTyping, typeSpeed.value);
};

onMounted(() => {
  handleTyping();
});

const experiences = [
  {
    period: "Aug 2024—Present",
    role: "Software Developer",
    company: "City of Armadale",
    description: "Led development of municipal websites using Next.js. Architected AWS infrastructure with CDK, managing S3, CloudFront, ECS, and CodePipeline.",
    tech: ["NextJS", "AWS", "Python", "TypeScript"]
  },
  {
    period: "Oct 2021—Aug 2024",
    role: "Snr. Software Engineer",
    company: "Elan Squared",
    description: "Built practice automation software for financial advisors using Java Spring and NuxtJS. Responsible for AWS infrastructure with TypeScript CDK. Mentored junior developers.",
    tech: ["Java Spring", "NuxtJS", "AWS", "MongoDB"]
  },
  {
    period: "Mar 2021—Oct 2021",
    role: "Software Engineer",
    company: "Pentanet",
    description: "Developed GeForce Now portal and internal management systems using Laravel framework with MySQL.",
    tech: ["PHP", "Laravel", "MySQL", "GCP"]
  },
  {
    period: "Nov 2019—Mar 2021",
    role: "Software Engineer",
    company: "Scantek Solutions",
    description: "Built ID verification software for multiple sectors. Developed OCR truthing interface and implemented WA Government Banned Drinker Register.",
    tech: ["PHP", "Node.js", "MongoDB", "AWS"]
  },
  {
    period: "Nov 2013—Feb 2019",
    role: "Software Developer",
    company: "Peoplefone AG",
    description: "Developed VoIP provisioning system serving multiple European countries. Led implementation of user/admin portal v2. Built internal tools for customer support optimization.",
    tech: ["Laravel", "PostgreSQL", "PHP"]
  }
];

const expertise = [
  {
    cat: "Frontend",
    icon: "lucide:monitor",
    skills: [
      {name: "NextJS", icon: "logos:nextjs-icon"},
      {name: "NuxtJS", icon: "logos:nuxt-icon"},
      {name: "React", icon: "logos:react"},
      {name: "Vue", icon: "logos:vue"},
      {name: "TypeScript", icon: "logos:typescript-icon"},
      {name: "JavaScript", icon: "logos:javascript"},
      {name: "Python", icon: "logos:python"}
    ]
  },
  {
    cat: "Backend",
    icon: "lucide:database",
    skills: [
      {name: "Laravel", icon: "logos:laravel"},
      {name: "Spring Boot", icon: "logos:spring-icon"},
      {name: "Node.js", icon: "logos:nodejs-icon"},
      {name: "PHP", icon: "logos:php"},
      {name: "Python", icon: "logos:python"}
    ]
  },
  {
    cat: "Cloud & DevOps",
    icon: "lucide:cloud",
    skills: [
      {name: "AWS", icon: "logos:aws"},
      {name: "Docker", icon: "logos:docker-icon"},
      {name: "CI/CD", icon: "lucide:git-pull-request"},
      {name: "GCP", icon: "logos:google-cloud"},
    ]
  },
  {
    cat: "Database",
    icon: "lucide:hard-drive",
    skills: [
      {name: "PostgreSQL", icon: "logos:postgresql"},
      {name: "MySQL", icon: "logos:mysql-icon"},
      {name: "MongoDB", icon: "logos:mongodb-icon"}
    ]
  }
];
</script>

<template>
  <div class="min-h-screen bg-zinc-50 selection:bg-zinc-900 selection:text-white">
    <section class="relative overflow-hidden">
      <div class="max-w-7xl mx-auto px-6 lg:px-12 py-20 lg:py-24">
        <div class="grid lg:grid-cols-12 gap-12 items-end mb-16">
          <div class="lg:col-span-8">
            <div class="inline-block mb-6 h-8">
              <div class="font-body text-sm uppercase tracking-wider text-zinc-500 mb-2 flex items-center min-h-[20px]">
                <span>{{ displayText || '\u200B' }}</span>
                <span class="ml-1 w-0.5 h-4 bg-zinc-400 animate-pulse"></span>
              </div>
              <div class="h-px bg-zinc-900 w-24"></div>
            </div>

            <h1 class="font-display text-7xl lg:text-9xl font-bold text-zinc-900 leading-[0.85]">
              Raoul<br/>Hofmann
            </h1>
          </div>

          <div class="lg:col-span-4 lg:flex lg:justify-end">
            <div class="bg-zinc-900 text-zinc-50 p-8 w-full lg:max-w-xs">
              <div class="font-body text-xs uppercase tracking-wider mb-4 text-zinc-400 flex items-center gap-2">
                <Icon class="w-3 h-3" name="lucide:map-pin"/>
                Location
              </div>
              <div class="font-display text-3xl font-bold">
                Perth, WA<br/>Australia
              </div>
            </div>
          </div>
        </div>

        <div class="grid lg:grid-cols-12 gap-12 border-t border-zinc-200 pt-8 pb-8">
          <div class="lg:col-span-12 font-body text-xl lg:text-3xl text-zinc-700 leading-tight space-y-6">
            <p>
              Throughout my career, I have always strived to provide software solutions that
              directly benefit stakeholders, taking great satisfaction in engaging with and
              understanding their needs to ensure that the solutions I develop have a meaningful impact.
            </p>
            <p>
              I thrive in the end to end delivery, implementation and continued
              improvement of business solutions tailored to evolving business needs.
            </p>
          </div>
        </div>
        <div>
          <div class="lg:col-span-4 flex flex-col justify-end gap-6 pt-6 lg:pt-0">
            <div class="flex flex-wrap gap-6 font-body text-sm">
              <a class="group flex items-center gap-2 text-zinc-900 hover:text-zinc-600 transition-colors"
                 href="mailto:raouldhofmann@gmail.com">
                <Icon class="w-2 h-2 fill-current" name="lucide:circle"/>
                raouldhofmann@gmail.com
              </a>
              <a class="group flex items-center gap-2 text-zinc-900 hover:text-zinc-600 transition-colors"
                 href="https://github.com/RaoulHofmann" target="_blank">
                <Icon class="w-2 h-2 fill-current" name="lucide:circle"/>
                GitHub
                <Icon class="w-4 h-4 group-hover:translate-x-0.5 group-hover:-translate-y-0.5 transition-transform"
                      name="lucide:arrow-up-right"/>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-white py-12">
      <div class="max-w-7xl mx-auto px-6 lg:px-12">
        <div class="flex items-baseline gap-4 mb-20">
          <div class="font-display text-5xl lg:text-6xl font-bold text-zinc-900">
            Experience
          </div>
          <div class="h-px bg-zinc-300 flex-1"></div>
        </div>

        <div class="space-y-12">
          <div
              v-for="(exp, idx) in experiences"
              :key="idx"
              class="grid lg:grid-cols-12 gap-8 lg:gap-12 group"
              @mouseenter="hoveredExp = idx"
              @mouseleave="hoveredExp = null"
          >
            <div class="lg:col-span-12">
              <div class="flex flex-col lg:flex-row lg:justify-between lg:items-start mb-6">
                <div>
                  <div class="font-body text-sm text-zinc-500 mb-2">
                    {{ exp.period }}
                  </div>
                  <h3 class="font-display text-4xl font-bold text-zinc-900 mb-2">
                    {{ exp.role }}
                  </h3>
                  <div class="font-body text-xl text-zinc-600">
                    {{ exp.company }}
                  </div>
                </div>
              </div>

              <p class="font-body text-lg text-zinc-700 leading-relaxed mb-6">
                {{ exp.description }}
              </p>

              <div class="flex flex-wrap gap-3">
                <span
                    v-for="(tech, i) in exp.tech"
                    :key="i"
                    class="font-body text-xs uppercase tracking-wider px-4 py-2 border border-zinc-900 text-zinc-900"
                >
                  {{ tech }}
                </span>
              </div>

              <div
                  :class="hoveredExp === idx ? 'w-full' : 'w-0'"
                  class="h-px bg-zinc-900 mt-12 transition-all duration-500"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-zinc-900 text-zinc-50 py-24">
      <div class="max-w-7xl mx-auto px-6 lg:px-12">
        <div class="flex items-baseline gap-8 mb-24">
          <h2 class="font-display text-5xl lg:text-7xl font-bold">Tech Stack</h2>
          <div class="h-px bg-zinc-800 flex-1"></div>
        </div>

        <div class="space-y-12">
          <div v-for="group in expertise" :key="group.cat" class="group/item">
            <div class="flex items-center gap-4 mb-8">
              <div class="p-2 border border-zinc-700 rounded-sm group-hover/item:border-zinc-500 transition-colors">
                <Icon :name="group.icon" class="w-5 h-5 text-zinc-400" />
              </div>
              <h3 class="font-body text-sm uppercase tracking-[0.2em] text-zinc-500 group-hover/item:text-zinc-300 transition-colors">
                {{ group.cat }}
              </h3>
            </div>

            <div class="flex flex-wrap gap-x-12 gap-y-10">
              <div v-for="skill in group.skills" :key="skill.name"
                   class="flex flex-col items-center gap-4 group/skill">
                <div class="relative">
                  <Icon :name="skill.icon"
                        class="w-10 h-10 grayscale opacity-40 group-hover/item:grayscale-0 group-hover/item:opacity-100 transition-all duration-700" />
                </div>
                <span class="font-display text-xl lg:text-2xl font-medium tracking-tight">
                  {{ skill.name }}
                </span>
              </div>
            </div>

            <div class="h-px bg-zinc-800/50 w-full mt-16"></div>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-white py-12">
      <div class="max-w-7xl mx-auto px-6 lg:px-12">
        <h2 class="font-display text-5xl lg:text-6xl font-bold text-zinc-900 mb-16">
          Education
        </h2>

        <div class="grid lg:grid-cols-2 gap-12">
          <div class="border-t-4 border-zinc-900 pt-8">
            <div class="font-body text-sm text-zinc-500 mb-4">2017—2019</div>
            <h3 class="font-display text-3xl font-bold text-zinc-900 mb-3">
              Bachelor of Science
            </h3>
            <div class="font-body text-xl text-zinc-700 mb-2">Computer Science</div>
            <div class="font-body text-zinc-600">Murdoch University, Perth WA</div>
          </div>

          <div class="border-t-4 border-zinc-900 pt-8">
            <div class="font-body text-sm text-zinc-500 mb-4">2009—2013</div>
            <h3 class="font-display text-3xl font-bold text-zinc-900 mb-3">
              Federal VET Diploma
            </h3>
            <div class="font-body text-xl text-zinc-700 mb-2">Information Technology</div>
            <div class="font-body text-zinc-600">T.B.Z, Zurich Switzerland</div>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-zinc-900 text-zinc-50 py-24">
      <div class="max-w-7xl mx-auto px-6 lg:px-12 text-center">
        <h2 class="font-display text-6xl lg:text-7xl font-bold mb-8">
          Let's Connect
        </h2>
        <p class="font-body text-xl text-zinc-400 mb-12 max-w-2xl mx-auto">
          Available for new opportunities and interesting projects
        </p>
        <div class="flex flex-col sm:flex-row gap-6 justify-center">
          <a
              class="group font-body px-12 py-5 bg-zinc-50 text-zinc-900 text-lg font-bold hover:bg-zinc-200 transition-colors inline-flex items-center justify-center gap-3"
              href="mailto:raouldhofmann@gmail.com"
          >
            Get in Touch
            <Icon class="w-5 h-5 group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform"
                  name="lucide:arrow-up-right"/>
          </a>
          <a
              class="group font-body px-12 py-5 border-2 border-zinc-50 text-zinc-50 text-lg font-bold hover:bg-zinc-50 hover:text-zinc-900 transition-colors inline-flex items-center justify-center gap-3"
              href="https://github.com/RaoulHofmann"
              rel="noopener noreferrer"
              target="_blank"
          >
            View GitHub
            <Icon class="w-5 h-5 group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform"
                  name="lucide:arrow-up-right"/>
          </a>
        </div>
      </div>
    </section>

    <footer class="bg-zinc-50 py-12 border-t border-zinc-200">
      <div class="max-w-7xl mx-auto px-6 lg:px-12 font-body text-sm text-zinc-600 text-center">
        © 2026 Raoul Hofmann
      </div>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@400;500;700&display=swap');

.font-display {
  font-family: 'Playfair Display', serif;
}

.font-body {
  font-family: 'DM Sans', sans-serif;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-slide-in {
  animation: slideIn 0.6s ease-out forwards;
}

@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}

.animate-pulse {
  animation: pulse 1s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>