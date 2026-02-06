<script setup>
const hoveredExp = ref(null);
const isMatrixMode = ref(false);

const titles = [
  "Software Developer",
  "Full Stack Engineer",
  "User Focused",
  "Mentor & Team Lead"
];

const matrixTitles = [
  ">_ SOFTWARE.DEVELOPER",
  ">_ FULL.STACK",
  ">_ MENTOR.PROTOCOL"
];

const displayText = ref("");
const isDeleting = ref(false);
const wordIndex = ref(0);
const typeSpeed = ref(100);

const handleTyping = () => {
  const currentTitles = isMatrixMode.value ? matrixTitles : titles;
  const currentFullText = currentTitles[wordIndex.value % currentTitles.length];

  if (isDeleting.value) {
    displayText.value = currentFullText.substring(0, displayText.value.length - 1);
    typeSpeed.value = 50;
  } else {
    displayText.value = currentFullText.substring(0, displayText.value.length + 1);
    typeSpeed.value = 150;
  }

  if (!isDeleting.value && displayText.value === currentFullText) {
    setTimeout(() => {
      isDeleting.value = true;
      typeSpeed.value = 500;
    }, 800)
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

const matrixCanvas = ref(null);
const miniMatrixCanvas = ref(null);
let matrixAnimation = null;
let miniMatrixAnimation = null;

const startMatrixRain = () => {
  if (!matrixCanvas.value) return;

  const canvas = matrixCanvas.value;
  const ctx = canvas.getContext('2d');

  canvas.width = window.innerWidth;
  canvas.height = 800;

  const chars = 'ﾊﾐﾋｰｳｼﾅﾓﾆｻﾜﾂｵﾘｱﾎﾃﾏｹﾒｴｶｷﾑﾕﾗｾﾈｽﾀﾇﾍ01';
  const fontSize = 14;
  const columns = canvas.width / fontSize;
  const drops = Array(Math.floor(columns)).fill(1);

  const draw = () => {
    ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.fillStyle = '#0f0';
    ctx.font = fontSize + 'px monospace';

    for (let i = 0; i < drops.length; i++) {
      const text = chars[Math.floor(Math.random() * chars.length)];
      ctx.fillText(text, i * fontSize, drops[i] * fontSize);

      if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
        drops[i] = 0;
      }
      drops[i]++;
    }
  };

  matrixAnimation = setInterval(draw, 33);
};

const startMiniMatrixRain = () => {
  if (!miniMatrixCanvas.value) return;

  const canvas = miniMatrixCanvas.value;
  const ctx = canvas.getContext('2d');

  // Set actual canvas size
  canvas.width = 32;
  canvas.height = 32;

  const chars = 'ﾊﾐﾋｰｳｼﾅﾓﾆｻﾜﾂｵﾘｱﾎﾃﾏｹﾒｴｶｷﾑﾕﾗｾﾈｽﾀﾇﾍ01';
  const fontSize = 8;
  const columns = canvas.width / fontSize;
  const drops = Array(Math.floor(columns)).fill(1);

  const draw = () => {
    ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.fillStyle = '#0f0';
    ctx.font = fontSize + 'px monospace';

    for (let i = 0; i < drops.length; i++) {
      const text = chars[Math.floor(Math.random() * chars.length)];
      ctx.fillText(text, i * fontSize, drops[i] * fontSize);

      if (drops[i] * fontSize > canvas.height && Math.random() > 0.95) {
        drops[i] = 0;
      }
      drops[i]++;
    }
  };

  miniMatrixAnimation = setInterval(draw, 50);
};

const stopMatrixRain = () => {
  if (matrixAnimation) {
    clearInterval(matrixAnimation);
    matrixAnimation = null;
  }
};

const stopMiniMatrixRain = () => {
  if (miniMatrixAnimation) {
    clearInterval(miniMatrixAnimation);
    miniMatrixAnimation = null;
  }
};

watch(isMatrixMode, (newVal) => {
  if (newVal) {
    nextTick(() => startMatrixRain());
    stopMiniMatrixRain();
  } else {
    stopMatrixRain();
    nextTick(() => startMiniMatrixRain());
  }
});

onMounted(() => {
  handleTyping();
  // Start mini matrix rain after a short delay to ensure canvas is ready
  setTimeout(() => {
    startMiniMatrixRain();
  }, 100);
});

onUnmounted(() => {
  stopMatrixRain();
  stopMiniMatrixRain();
});

const toggleMatrixMode = () => {
  isMatrixMode.value = !isMatrixMode.value;
  // Reset typing animation
  displayText.value = "";
  isDeleting.value = false;
  wordIndex.value = 0;
};

const experiences = [
  {
    period: "Aug 2024—Present",
    matrixPeriod: "[2024.08 -> ACTIVE]",
    role: "Software Developer",
    matrixRole: "DEVELOPER.EXE",
    company: "City of Armadale",
    matrixCompany: "CITY.ARMADALE",
    description: "Led development of municipal websites using Next.js. Architected AWS infrastructure with CDK, managing S3, CloudFront, ECS, and CodePipeline.",
    matrixDescription: ">> EXECUTE: Municipal web protocols via Next.js || AWS infrastructure deployment: S3 > CloudFront > ECS > CodePipeline || STATUS: OPERATIONAL",
    tech: ["NextJS", "AWS", "Python", "TypeScript"],
    matrixTech: ["[NEXT.JS]", "[AWS.CLOUD]", "[PY.THON]", "[TYPE.SCRIPT]"]
  },
  {
    period: "Oct 2021—Aug 2024",
    matrixPeriod: "[2021.10 -> 2024.08]",
    role: "Snr. Software Engineer",
    matrixRole: "SENIOR.ENGINEER.EXE",
    company: "Elan Squared",
    matrixCompany: "ELAN.SQUARED",
    description: "Built practice automation software for financial advisors using Java Spring and NuxtJS. Responsible for AWS infrastructure with TypeScript CDK. Mentored junior developers.",
    matrixDescription: ">> COMPILE: Financial automation protocols || FRAMEWORK: Java.Spring + Nuxt.JS || DEPLOY: AWS.CDK >> TypeScript || MENTOR.PROTOCOL: Junior.Devs >> ACTIVE",
    tech: ["Java Spring", "NuxtJS", "AWS", "MongoDB"],
    matrixTech: ["[JAVA.SPRING]", "[NUXT.JS]", "[AWS.CLOUD]", "[MONGO.DB]"]
  },
  {
    period: "Mar 2021—Oct 2021",
    matrixPeriod: "[2021.03 -> 2021.10]",
    role: "Software Engineer",
    matrixRole: "ENGINEER.EXE",
    company: "Pentanet",
    matrixCompany: "PENTA.NET",
    description: "Developed GeForce Now portal and internal management systems using Laravel framework with MySQL.",
    matrixDescription: ">> INITIALIZE: GeForce.Now portal >> Laravel.Framework >> MySQL.Database >> Internal.Management.Systems >> COMPILE_SUCCESS",
    tech: ["PHP", "Laravel", "MySQL", "GCP"],
    matrixTech: ["[PHP.LANG]", "[LARAVEL.FW]", "[MY.SQL]", "[GCP.CLOUD]"]
  },
  {
    period: "Nov 2019—Mar 2021",
    matrixPeriod: "[2019.11 -> 2021.03]",
    role: "Software Engineer",
    matrixRole: "ENGINEER.EXE",
    company: "Scantek Solutions",
    matrixCompany: "SCANTEK.SOLUTIONS",
    description: "Built ID verification software for multiple sectors. Developed OCR truthing interface and implemented WA Government Banned Drinker Register.",
    matrixDescription: ">> RUN: ID_Verification.Multi_Sector >> OCR.Interface >> DEPLOY: WA.Gov.BannedDrinker.Register >> VERIFICATION_COMPLETE",
    tech: ["PHP", "Node.js", "MongoDB", "AWS"],
    matrixTech: ["[PHP.LANG]", "[NODE.JS]", "[MONGO.DB]", "[AWS.CLOUD]"]
  },
  {
    period: "Nov 2013—Feb 2019",
    matrixPeriod: "[2013.11 -> 2019.02]",
    role: "Software Developer",
    matrixRole: "DEVELOPER.EXE",
    company: "Peoplefone AG",
    matrixCompany: "PEOPLEFONE.AG",
    description: "Developed VoIP provisioning system serving multiple European countries. Led implementation of user/admin portal v2. Built internal tools for customer support optimization.",
    matrixDescription: ">> BOOT: VoIP.Provisioning >> EU.Multi_Country >> DEPLOY: Portal.v2 >> User.Admin.Interface >> Support.Tools >> OPTIMIZATION_ACTIVE",
    tech: ["Laravel", "PostgreSQL", "PHP"],
    matrixTech: ["[LARAVEL.FW]", "[POSTGRE.SQL]", "[PHP.LANG]"]
  }
];

const expertise = [
  {
    cat: "Frontend",
    matrixCat: "FRONTEND.SYS",
    icon: "lucide:monitor",
    skills: [
      {name: "NextJS", matrixName: "NEXT.JS", icon: "logos:nextjs-icon"},
      {name: "NuxtJS", matrixName: "NUXT.JS", icon: "logos:nuxt-icon"},
      {name: "React", matrixName: "REACT.LIB", icon: "logos:react"},
      {name: "Vue", matrixName: "VUE.JS", icon: "logos:vue"},
      {name: "TypeScript", matrixName: "TYPE.SCRIPT", icon: "logos:typescript-icon"},
      {name: "JavaScript", matrixName: "JAVA.SCRIPT", icon: "logos:javascript"},
      {name: "Python", matrixName: "PY.THON", icon: "logos:python"}
    ]
  },
  {
    cat: "Backend",
    matrixCat: "BACKEND.SYS",
    icon: "lucide:database",
    skills: [
      {name: "Laravel", matrixName: "LARAVEL.FW", icon: "logos:laravel"},
      {name: "Spring Boot", matrixName: "SPRING.BOOT", icon: "logos:spring-icon"},
      {name: "Node.js", matrixName: "NODE.JS", icon: "logos:nodejs-icon"},
      {name: "PHP", matrixName: "PHP.LANG", icon: "logos:php"},
      {name: "Python", matrixName: "PY.THON", icon: "logos:python"}
    ]
  },
  {
    cat: "Cloud & DevOps",
    matrixCat: "CLOUD.OPS",
    icon: "lucide:cloud",
    skills: [
      {name: "AWS", matrixName: "AWS.CLOUD", icon: "logos:aws"},
      {name: "Docker", matrixName: "DOCKER.CONTAINER", icon: "logos:docker-icon"},
      {name: "CI/CD", matrixName: "CI.CD.PIPELINE", icon: "lucide:git-pull-request"},
      {name: "GCP", matrixName: "GCP.CLOUD", icon: "logos:google-cloud"},
    ]
  },
  {
    cat: "Database",
    matrixCat: "DATABASE.SYS",
    icon: "lucide:hard-drive",
    skills: [
      {name: "PostgreSQL", matrixName: "POSTGRE.SQL", icon: "logos:postgresql"},
      {name: "MySQL", matrixName: "MY.SQL", icon: "logos:mysql-icon"},
      {name: "MongoDB", matrixName: "MONGO.DB", icon: "logos:mongodb-icon"}
    ]
  }
];
</script>

<template>
  <div :class="isMatrixMode ? 'matrix-mode' : ''"
       :style="isMatrixMode ? 'background: #000' : 'background: rgb(250 250 250)'"
       class="min-h-screen transition-all duration-500">

    <canvas v-show="isMatrixMode" ref="matrixCanvas" class="fixed inset-0 pointer-events-none z-0"></canvas>

    <div class="relative z-10">
      <section class="relative overflow-hidden">
        <div class="max-w-7xl mx-auto px-6 lg:px-12 py-20 lg:py-24">
          <div class="grid lg:grid-cols-12 gap-12 items-end mb-16">
            <div class="lg:col-span-8">
              <div class="inline-block mb-6">
                <div class="flex items-center gap-3 mb-2">
                  <div :class="isMatrixMode ? 'matrix-text font-mono' : 'font-body'"
                       :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(113 113 122)'"
                       class="text-sm uppercase tracking-wider flex items-center min-h-[20px]">
                    <span>{{ displayText || '\u200B' }}</span>
                    <span :style="isMatrixMode ? 'background: #0f0' : 'background: rgb(161 161 170)'"
                          class="ml-1 w-0.5 h-4 animate-pulse"></span>
                  </div>

                </div>
                <div :style="isMatrixMode ? 'background: #0f0' : 'background: rgb(24 24 27)'" class="h-px w-24"></div>
              </div>

              <h1 :class="isMatrixMode ? 'matrix-title font-mono' : 'font-display'"
                  :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(24 24 27)'"
                  class="text-7xl lg:text-9xl font-bold leading-[0.85]">
                <template v-if="!isMatrixMode">Raoul<br/>Hofmann</template>
                <template v-else>
                  <div class="text-4xl lg:text-6xl leading-tight">
                    R A O U L<br/>
                    H O F M A N N
                  </div>
                </template>
              </h1>
            </div>

            <div class="lg:col-span-4 lg:flex lg:justify-end flex-col">
              <div class="flex justify-end w-full">
                <!-- Matrix Mode Toggle -->
                <button
                    :class="isMatrixMode ? 'matrix-toggle-active' : 'matrix-toggle'"
                    class="group relative"
                    title="Toggle Matrix Mode"
                    @click="toggleMatrixMode"
                >
                  <canvas v-if="!isMatrixMode"
                          ref="miniMatrixCanvas"
                          class="w-8 h-8 rounded"
                          style="background: #000"></canvas>
                  <Icon v-else class="w-4 h-4 matrix-icon" name="lucide:x"/>
                </button>
              </div>
              <div :class="isMatrixMode ? 'matrix-box' : 'bg-zinc-900 text-zinc-50'"
                   class="p-8 w-full lg:max-w-md">
                <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body'"
                     :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(161 161 170)'"
                     class="text-xs uppercase tracking-wider mb-4 flex items-center gap-2">
                  <Icon class="w-3 h-3" name="lucide:map-pin"/>
                  <span v-if="!isMatrixMode">Location</span>
                  <span v-else>COORDINATES</span>
                </div>
                <div :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display'"
                     :style="isMatrixMode ? 'color: #0f0' : ''"
                     class="text-3xl font-bold">
                  <span v-if="!isMatrixMode">Perth, WA<br/>Australia</span>
                  <span v-else>-31.9505<br/>115.8605</span>
                </div>
              </div>
            </div>
          </div>

          <div :style="isMatrixMode ? 'border-color: #0f0' : 'border-color: rgb(228 228 231)'"
               class="grid lg:grid-cols-12 gap-12 border-t pt-8 pb-8">
            <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-700'"
                 class="lg:col-span-12 text-xl lg:text-3xl leading-tight space-y-6">
              <p v-if="!isMatrixMode">
                Throughout my career, I have always strived to provide software solutions that
                directly benefit stakeholders, taking great satisfaction in engaging with and
                understanding their needs to ensure that the solutions I develop have a meaningful impact.
              </p>
              <p v-if="!isMatrixMode">
                I thrive in the end to end delivery, implementation and continued
                improvement of business solutions tailored to evolving business needs.
              </p>

              <p v-if="isMatrixMode" class="text-lg lg:text-xl">
                >> MISSION_STATEMENT: Deploying software solutions with maximum stakeholder impact
                <br/>>> PROTOCOL: Engage.Analyze.Develop.Deploy
                <br/>>> CORE_FUNCTION: End-to-end delivery systems optimized for evolving business parameters
              </p>
            </div>
          </div>
          <div>
            <div class="lg:col-span-4 flex flex-col justify-end gap-6 pt-6 lg:pt-0">
              <div :class="isMatrixMode ? 'font-mono matrix-links' : 'font-body'"
                   class="flex flex-wrap gap-6 text-sm">
                <a :class="isMatrixMode ? 'matrix-link' : 'text-zinc-900 hover:text-zinc-600'"
                   class="group flex items-center gap-2 transition-colors"
                   href="mailto:raouldhofmann@gmail.com">
                  <Icon class="w-2 h-2 fill-current" name="lucide:circle"/>
                  <span v-if="!isMatrixMode">raouldhofmann@gmail.com</span>
                  <span v-else>raouldhofmann[@]gmail.com</span>
                </a>
                <a :class="isMatrixMode ? 'matrix-link' : 'text-zinc-900 hover:text-zinc-600'"
                   class="group flex items-center gap-2 transition-colors"
                   href="https://github.com/RaoulHofmann" target="_blank">
                  <Icon class="w-2 h-2 fill-current" name="lucide:circle"/>
                  <span v-if="!isMatrixMode">GitHub</span>
                  <span v-else>github.com/RaoulHofmann</span>
                  <Icon class="w-4 h-4 group-hover:translate-x-0.5 group-hover:-translate-y-0.5 transition-transform"
                        name="lucide:arrow-up-right"/>
                </a>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section :class="isMatrixMode ? 'matrix-section' : 'bg-white'" class="py-12">
        <div class="max-w-7xl mx-auto px-6 lg:px-12">
          <div class="flex items-baseline gap-4 mb-20">
            <h2 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display'"
                 :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(24 24 27)'"
                 class="text-5xl lg:text-6xl font-bold">
              <span v-if="!isMatrixMode">Experience</span>
              <span v-else>>> WORK.HISTORY</span>
            </h2>
            <div :style="isMatrixMode ? 'background: #0f0' : 'background: rgb(212 212 216)'" class="h-px flex-1"></div>
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
                    <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-500'"
                         class="text-sm mb-2">
                      {{ isMatrixMode ? exp.matrixPeriod : exp.period }}
                    </div>
                    <h3 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display'"
                        :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(24 24 27)'"
                        class="text-4xl font-bold mb-2">
                      {{ isMatrixMode ? exp.matrixRole : exp.role }}
                    </h3>
                    <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body'"
                         :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(82 82 91)'"
                         class="text-xl">
                      {{ isMatrixMode ? exp.matrixCompany : exp.company }}
                    </div>
                  </div>
                </div>

                <p :class="isMatrixMode ? 'font-mono matrix-text text-base' : 'font-body text-zinc-700'"
                   class="text-lg leading-relaxed mb-6">
                  {{ isMatrixMode ? exp.matrixDescription : exp.description }}
                </p>

                <div class="flex flex-wrap gap-3">
                  <span
                      v-for="(tech, i) in (isMatrixMode ? exp.matrixTech : exp.tech)"
                      :key="i"
                      :class="isMatrixMode ? 'matrix-tag' : 'border-zinc-900 text-zinc-900'"
                      class="font-body text-xs uppercase tracking-wider px-4 py-2 border"
                  >
                    {{ tech }}
                  </span>
                </div>

                <div
                    :class="hoveredExp === idx ? 'w-full' : 'w-0'"
                    :style="isMatrixMode ? 'background: #0f0' : 'background: rgb(24 24 27)'"
                    class="h-px mt-12 transition-all duration-500"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section :class="isMatrixMode ? 'matrix-dark-section' : 'bg-zinc-900 text-zinc-50'" class="py-24">
        <div class="max-w-7xl mx-auto px-6 lg:px-12">
          <div class="flex items-baseline gap-8 mb-24">
            <h2 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display text-zinc-50'"
                class="text-5xl lg:text-6xl font-bold">
              <span v-if="!isMatrixMode">Tech Stack</span>
              <span v-else>>> TECH.ARSENAL</span>
            </h2>
            <div :style="isMatrixMode ? 'background: #0f0' : 'background: rgb(39 39 42)'" class="h-px flex-1"></div>
          </div>

          <div class="space-y-12">
            <div v-for="group in expertise" :key="group.cat" class="group/item">
              <div class="flex items-center gap-4 mb-8">
                <div :class="isMatrixMode ? 'matrix-icon-box' : 'border-zinc-700 group-hover/item:border-zinc-500'"
                     class="p-2 border rounded-sm transition-colors flex justify-center items-center">
                  <Icon :name="group.icon" :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(161 161 170)'"
                        class="w-5 h-5"/>
                </div>
                <h3 :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-500 group-hover/item:text-zinc-300'"
                    class="text-sm uppercase tracking-[0.2em] transition-colors">
                  {{ isMatrixMode ? group.matrixCat : group.cat }}
                </h3>
              </div>

              <div class="flex flex-wrap gap-x-12 gap-y-10 max-md:justify-center">
                <div v-for="skill in group.skills" :key="skill.name"
                     class="flex flex-col items-center gap-4 group/skill">
                  <div class="relative">
                    <Icon
                        :class="isMatrixMode ? 'matrix-skill-icon' : 'grayscale opacity-40 group-hover/item:grayscale-0 group-hover/item:opacity-100 max-md:grayscale-0 max-md:opacity-100'"
                        :name="skill.icon"
                        class="w-10 h-10 transition-all duration-700"/>
                  </div>
                  <span
                      :class="isMatrixMode ? 'font-mono matrix-text text-lg' : 'font-display text-zinc-50 text-xl lg:text-2xl'"
                      class="font-medium tracking-tight">
                    {{ isMatrixMode ? skill.matrixName : skill.name }}
                  </span>
                </div>
              </div>

              <div :style="isMatrixMode ? 'background: rgba(0, 255, 0, 0.3)' : 'background: rgba(39, 39, 42, 0.5)'"
                   class="h-px w-full mt-16"></div>
            </div>
          </div>
        </div>
      </section>

      <section :class="isMatrixMode ? 'matrix-section' : 'bg-white'" class="py-12">
        <div class="max-w-7xl mx-auto px-6 lg:px-12">
          <div class="flex items-baseline gap-4 mb-20">
            <h2 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display'"
                 :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(24 24 27)'"
                 class="text-5xl lg:text-6xl font-bold">
              <span v-if="!isMatrixMode">Education</span>
              <span v-else>>> TRAINING.LOG</span>
            </h2>
            <div :style="isMatrixMode ? 'background: #0f0' : 'background: rgb(212 212 216)'" class="h-px flex-1"></div>
          </div>

          <div class="grid lg:grid-cols-2 gap-12">
            <div :style="isMatrixMode ? 'border-color: #0f0' : 'border-color: rgb(24 24 27)'"
                 class="md:border-t-4 sm:pt-8">
              <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-500'" class="text-sm mb-4">
                <span v-if="!isMatrixMode">2017—2019</span>
                <span v-else">[2017 -> 2019]</span>
              </div>
              <h3 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display'"
                  :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(24 24 27)'"
                  class="text-3xl font-bold mb-3">
                <span v-if="!isMatrixMode">Bachelor of Science</span>
                <span v-else>BSc.DEGREE</span>
              </h3>
              <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-700'" class="text-xl mb-2">
                <span v-if="!isMatrixMode">Computer Science</span>
                <span v-else>Computer.Science.Protocol</span>
              </div>
              <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-600'">
                <span v-if="!isMatrixMode">Murdoch University, Perth WA</span>
                <span v-else>Murdoch.Uni >> Perth.WA</span>
              </div>
            </div>

            <div :style="isMatrixMode ? 'border-color: #0f0' : 'border-color: rgb(24 24 27)'" class="border-t-4 pt-8">
              <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-500'" class="text-sm mb-4">
                <span v-if="!isMatrixMode">2009—2013</span>
                <span v-else>[2009 -> 2013]</span>
              </div>
              <h3 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display'"
                  :style="isMatrixMode ? 'color: #0f0' : 'color: rgb(24 24 27)'"
                  class="text-3xl font-bold mb-3">
                <span v-if="!isMatrixMode">Federal VET Diploma</span>
                <span v-else">VET.DIPLOMA</span>
              </h3>
              <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-700'" class="text-xl mb-2">
                <span v-if="!isMatrixMode">Information Technology</span>
                <span v-else>Software.Engineering</span>
              </div>
              <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-600'">
                <span v-if="!isMatrixMode">T.B.Z, Zurich Switzerland</span>
                <span v-else>T.B.Z >> Zurich.CH</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section :class="isMatrixMode ? 'matrix-dark-section' : 'bg-zinc-900 text-zinc-50'" class="py-24">
        <div class="max-w-7xl mx-auto px-6 lg:px-12 text-center">
          <h2 :class="isMatrixMode ? 'font-mono matrix-glow' : 'font-display text-zinc-50'"
              class="text-6xl lg:text-7xl font-bold mb-8">
            <span v-if="!isMatrixMode">Let's Connect</span>
            <span v-else>>> INITIATE.CONTACT</span>
          </h2>
          <p :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-400'"
             class="text-xl mb-12 max-w-2xl mx-auto">
            <span v-if="!isMatrixMode">Available for new opportunities and interesting projects</span>
            <span v-else>STATUS: Available for deployment on new projects</span>
          </p>
          <div class="flex flex-col sm:flex-row gap-6 justify-center">
            <a
                :class="isMatrixMode ? 'matrix-button' : 'bg-zinc-50 text-zinc-900 hover:bg-zinc-200'"
                class="group font-body px-12 py-5 text-lg font-bold transition-colors inline-flex items-center justify-center gap-3"
                href="mailto:raouldhofmann@gmail.com"
            >
              <span v-if="!isMatrixMode">Get in Touch</span>
              <span v-else class="font-mono">SEND.MESSAGE</span>
              <Icon class="w-5 h-5 group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform"
                    name="lucide:arrow-up-right"/>
            </a>
            <a
                :class="isMatrixMode ? 'matrix-button-outline' : 'border-2 border-zinc-50 text-zinc-50 hover:bg-zinc-50 hover:text-zinc-900'"
                class="group font-body px-12 py-5 text-lg font-bold transition-colors inline-flex items-center justify-center gap-3"
                href="https://github.com/RaoulHofmann"
                rel="noopener noreferrer"
                target="_blank"
            >
              <span v-if="!isMatrixMode">View GitHub</span>
              <span v-else class="font-mono">ACCESS.REPO</span>
              <Icon class="w-5 h-5 group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform"
                    name="lucide:arrow-up-right"/>
            </a>
          </div>
        </div>
      </section>

      <footer :class="isMatrixMode ? 'matrix-footer' : 'bg-zinc-50'"
              :style="isMatrixMode ? 'border-color: #0f0' : 'border-color: rgb(228 228 231)'"
              class="py-4 border-t">
        <div :class="isMatrixMode ? 'font-mono matrix-text' : 'font-body text-zinc-600'"
             class="max-w-7xl mx-auto text-sm text-center">
          <span v-if="!isMatrixMode">© 2026 Raoul Hofmann</span>
          <span v-else>© 2026 >> RAOUL.HOFMANN >> ALL_RIGHTS_RESERVED</span>
        </div>
      </footer>
    </div>
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

/* Matrix Mode Styles */
.matrix-mode {
  background: #000 !important;
}

.matrix-text {
  color: #0f0;
  text-shadow: 0 0 5px #0f0;
}

.matrix-glow {
  color: #0f0;
  text-shadow: 0 0 10px #0f0, 0 0 20px #0f0, 0 0 30px #0f0;
}

.matrix-box {
  background: #000;
  border: 2px solid #0f0;
  box-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
}

.matrix-section {
  background: #000;
}

.matrix-dark-section {
  background: #001100;
  border-top: 1px solid #0f0;
  border-bottom: 1px solid #0f0;
}

.matrix-link {
  color: #0f0;
  text-shadow: 0 0 5px #0f0;
}

.matrix-link:hover {
  color: #0ff;
  text-shadow: 0 0 10px #0ff;
}

.matrix-tag {
  border: 1px solid #0f0 !important;
  color: #0f0 !important;
  background: rgba(0, 255, 0, 0.1);
  font-family: 'Courier New', monospace;
}

.matrix-icon-box {
  border: 1px solid #0f0;
  background: rgba(0, 255, 0, 0.1);
}

.matrix-skill-icon {
  //filter: brightness(0) saturate(100%) invert(50%) sepia(100%) hue-rotate(90deg);
}

.matrix-button {
  background: #0f0;
  color: #000;
  font-family: 'Courier New', monospace;
}

.matrix-button:hover {
  background: #0ff;
  border-color: #0ff;
  box-shadow: 0 0 20px rgba(0, 255, 255, 0.8);
}

.matrix-button-outline {
  background: transparent;
  color: #0f0;
  font-family: 'Courier New', monospace;
}

.matrix-button-outline:hover {
  background: #0f0;
  color: #000;
  box-shadow: 0 0 20px rgba(0, 255, 0, 0.8);
}

.matrix-footer {
  background: #000;
  border-top: 1px solid #0f0;
}

.matrix-toggle {
  background: transparent;
  margin-bottom: 0.75rem;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.3s;
  position: relative;
}

.matrix-toggle:hover {
  background: rgb(24 24 27);
  color: white;
}

.matrix-toggle-active {
  background: transparent;
  margin-bottom: 0.75rem;
  cursor: pointer;
  position: relative;
}

.matrix-icon {
  color: #0f0;
  text-shadow: 0 0 10px #0f0;
}

.matrix-title {
  letter-spacing: 0.05em;
  line-height: 1.1;
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