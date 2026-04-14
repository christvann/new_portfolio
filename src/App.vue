<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="nav-logo">
        <div class="logo-circle">
          <span class="logo-letter">I</span>
        </div>
        <span class="logo-text">Ivan Christian</span>
      </div>

      <div class="nav-links">
        <a href="#about" :class="['nav-item', { active: activeSection === 'about' }]">About</a>
        <a href="#work" :class="['nav-item', { active: activeSection === 'work' }]">Work</a>
        <a href="#projects" :class="['nav-item', { active: activeSection === 'projects' }]"
          >Projects</a
        >
        <a href="#contact" :class="['nav-item', { active: activeSection === 'contact' }]"
          >Contact</a
        >
      </div>
    </div>
  </nav>
  <div v-if="isDesktop">
    <div class="cursor-glow" :style="{ left: cursorX + 'px', top: cursorY + 'px' }"></div>

    <div class="cursor-dot" :style="{ left: cursorX + 'px', top: cursorY + 'px' }"></div>
  </div>

  <main class="container">
    <section id="about" class="hero-section">
      <div class="hero-content">
        <h2 class="role-title">Frontend Dev | Aspiring Fullstack Dev | AI Researcher</h2>
        <h1 class="main-name">Ivan Christian</h1>
        <p class="bio">
          Informatics Engineering graduate from <strong>Institut Teknologi PLN</strong> with a GPA
          of 3.50. Experienced as a Front-End Developer at PLN Icon Plus. Skilled in HTML, CSS,
          JavaScript, Vue.js, React.js, Three.js and Tailwind CSS for building responsive and
          scalable web applications, alongside a strong foundation in UI/UX design and Machine
          Learning (CNN).
        </p>
      </div>

      <div ref="canvasContainer" class="canvas-3d-container"></div>
    </section>
    <section id="work" class="experience-section">
      <h3 class="section-title">Experience & Education</h3>

      <div class="timeline-horizontal-wrapper">
        <div class="timeline-line-hz"></div>

        <div class="timeline-horizontal-container">
          <div class="timeline-item-hz" v-for="(exp, index) in experiences" :key="index">
            <div class="timeline-dot-hz"></div>

            <div class="exp-card-container">
              <div
                class="exp-card"
                :ref="
                  (el) => {
                    if (el) cardRefs[index] = el
                  }
                "
                @mousemove="handleMouseMove($event, index)"
                @mouseleave="handleMouseLeave(index)"
              >
                <div class="date-badge parallax-item-high">
                  <span class="badge-subtitle">{{ exp.badgeTop }}</span>
                  <span class="badge-title">{{ exp.badgeBottom }}</span>
                </div>

                <h4 class="exp-title parallax-item">{{ exp.title }}</h4>

                <ul class="exp-desc-list parallax-item">
                  <li v-for="(point, i) in exp.description" :key="i">
                    {{ point }}
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="skills-section">
      <h3 class="section-title">Core Capabilities</h3>
      <div class="skills-grid">
        <div v-for="(skill, index) in skills" :key="index" class="glow-card">
          <i :class="skill.icon" class="skill-icon"></i>
          <span>{{ skill.name }}</span>
        </div>
      </div>
    </section>

    <section id="projects" class="projects-section">
      <h3 class="section-title">Projects</h3>

      <div
        class="carousel-3d-wrapper"
        @touchstart="handleTouchStart"
        @touchend="handleTouchEnd"
        @mousedown="handleMouseDown"
        @mousemove="handleMouseMove"
        @mouseup="handleMouseUp"
        @mouseleave="handleMouseUp"
      >
        <button class="nav-btn prev" @click="prevSlide">❮</button>
        <button class="nav-btn next" @click="nextSlide">❯</button>

        <div class="carousel-3d-container">
          <article
            v-for="(project, index) in projects"
            :key="index"
            class="project-3d-card"
            :class="getCardClass(index)"
            @click="goToSlide(index)"
          >
            <div class="card-glow-effect"></div>
            <div class="project-content">
              <div class="project-image-wrapper">
                <img :src="project.image" :alt="project.name" class="project-img-display" />
                <div class="img-overlay"></div>
              </div>

              <div class="project-details-overlay">
                <span class="project-date">{{ project.category }}</span>
                <h4 class="project-name">{{ project.name }}</h4>
                <p class="project-desc">{{ project.description }}</p>

                <div class="project-footer">
                  <a
                    :href="project.github"
                    target="_blank"
                    class="github-icon-link"
                    @click.stop
                    title="View Source on GitHub"
                  >
                    <i class="devicon-github-original"></i>
                  </a>
                </div>
              </div>
            </div>
          </article>
        </div>

        <button class="nav-btn next" @click="nextSlide">❯</button>
      </div>

      <div class="carousel-3d-indicators">
        <span
          v-for="(_, index) in projects"
          :key="'dot-' + index"
          class="dot"
          :class="{ active: activeSlide === index }"
          @click="goToSlide(index)"
        ></span>
      </div>
    </section>
    <section id="contact" class="contact-section">
      <div class="contact-container">
        <div class="contact-info">
          <h2 class="contact-title">LET'S <br /><span class="highlight">CONNECT</span></h2>
          <p class="contact-subtitle">
            Have a project in mind or just want to say hi? <br />
            Feel free to reach out through any of the platforms below.
          </p>

          <div class="social-links">
            <a href="mailto:ivanvan0562@gmail.com" class="social-item" title="Email Me">
              <i class="devicon-google-plain"></i>
            </a>

            <a
              href="https://www.linkedin.com/in/ivan-christian-7683882a3/"
              target="_blank"
              class="social-item"
              title="LinkedIn"
            >
              <i class="devicon-linkedin-plain"></i>
            </a>

            <a
              href="https://github.com/christvann"
              target="_blank"
              class="social-item"
              title="GitHub"
            >
              <i class="devicon-github-original"></i>
            </a>

            <a
              href="https://www.instagram.com/chrstianvann/"
              target="_blank"
              class="social-item instagram-svg"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="32"
                height="32"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
              </svg>
            </a>
          </div>
        </div>

        <div class="contact-action">
          <div class="location-tag">
            <span>Based in Jakarta, Indonesia</span>
          </div>

          <a href="mailto:ivanvan0562@gmail.com" class="main-contact-btn">
            START A CONVERSATION
            <span class="btn-arrow">→</span>
          </a>

          <div class="availability">
            <span class="status-dot"></span>
            Available for freelance & full-time roles
          </div>
        </div>
      </div>

      <footer class="mini-footer">
        <p>&copy; 2026 IVAN CHRISTIAN. ALL RIGHTS RESERVED.</p>
      </footer>
    </section>
  </main>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const cardRefs = ref([])

const startX = ref(0);
const isDragging = ref(false);

const handleMouseDown = (e) => {
  isDragging.value = true;
  startX.value = e.clientX;
};

const handleMouseUp = (e) => {
  if (!isDragging.value) return;
  
  const endX = e.clientX;
  const difference = startX.value - endX;
  const threshold = 50; // Jarak geser minimal 50px

  if (Math.abs(difference) > threshold) {
    if (difference > 0) {
      nextSlide();
    } else {
      prevSlide();
    }
  }
  
  isDragging.value = false;
};

const handleMouseMove = (e, index) => {
  const card = cardRefs.value[index]
  if (!card) return

  // Dapatkan dimensi dan posisi kartu
  const rect = card.getBoundingClientRect()

  // Hitung posisi kursor relatif terhadap kartu
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top

  // Cari titik tengah kartu
  const centerX = rect.width / 2
  const centerY = rect.height / 2

  // Hitung derajat rotasi (Bagi dengan angka yang lebih besar untuk efek lebih halus)
  const rotateX = ((y - centerY) / centerY) * -15
  const rotateY = ((x - centerX) / centerX) * 15

  // Aplikasikan ke CSS
  card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale3d(1.02, 1.02, 1.02)`
}

const handleMouseLeave = (index) => {
  const card = cardRefs.value[index]
  if (!card) return

  card.style.transform = `perspective(1000px) rotateX(0deg) rotateY(0deg) scale3d(1, 1, 1)`
}

const cursorX = ref(0)
const cursorY = ref(0)
const isDesktop = ref(true)

const updateCursor = (e) => {
  requestAnimationFrame(() => {
    cursorX.value = e.clientX
    cursorY.value = e.clientY
  })
}

// --- DATA EXPERIENCE & EDUCATION ---
const experiences = ref([
  {
    badgeTop: 'EDUCATION',
    badgeBottom: '2021-2025',
    title: 'Institut Teknologi PLN (IT-PLN)',
    description: [
      'Bachelor of Informatics Engineering with a GPA of 3.50/4.00.',
      'Completed 10+ software and web development projects.',
      'Certified in Microsoft Office Specialist and Azure AI Fundamentals.',
    ],
  },
  {
    badgeTop: 'WORK',
    badgeBottom: 'Aug-Nov 2024',
    title: 'Front End Developer Intern (PLN Icon Plus)',
    description: [
      'Developed 10+ responsive UI components for the Diamond internal application.',
      'Built and maintained 5+ core application dashboards for Manager, Staff, and Admin roles.',
      'Collaborated with cross-functional teams to deliver UI features.',
    ],
  },
  {
    badgeTop: 'WORK',
    badgeBottom: '2023-2024',
    title: 'Student Mentor/Co-Mentor (IT-PLN)',
    description: [
      'Provided mentoring and guidance to 10+ students in leadership programs.',
      'Facilitated group discussions and training sessions for skill development.',
      'Assisted mentees in goal setting and progress monitoring.',
    ],
  },
])

import * as THREE from 'three'

// --- SETUP 3D (MEMORY SAFE MODE) ---
const canvasContainer = ref(null)
let scene, camera, renderer, object3D, animationId

const init3D = () => {
  if (!canvasContainer.value) return

  // 1. Scene & Camera
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(
    75,
    canvasContainer.value.clientWidth / canvasContainer.value.clientHeight,
    0.1,
    1000,
  )
  camera.position.z = 5

  renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true })
  renderer.setSize(canvasContainer.value.clientWidth, canvasContainer.value.clientHeight)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  canvasContainer.value.appendChild(renderer.domElement)

  const geometry = new THREE.IcosahedronGeometry(2, 1)
  const material = new THREE.MeshBasicMaterial({
    color: 0xe60000, // Warna Merah Neon
    wireframe: true,
    transparent: true,
    opacity: 0.6,
  })

  object3D = new THREE.Mesh(geometry, material)
  scene.add(object3D)

  // 4. Animasi Loop
  const animate = () => {
    animationId = requestAnimationFrame(animate)

    // Rotasi perlahan
    object3D.rotation.x += 0.002
    object3D.rotation.y += 0.003

    renderer.render(scene, camera)
  }
  animate()
}

// Cleanup saat komponen dihancurkan (Mencegah Memory Leak di Android)
const cleanup3D = () => {
  if (animationId) cancelAnimationFrame(animationId)
  if (renderer) renderer.dispose()
  if (object3D) {
    object3D.geometry.dispose()
    object3D.material.dispose()
  }
}

// Handle Resize Window
const handleResize = () => {
  if (camera && renderer && canvasContainer.value) {
    camera.aspect = canvasContainer.value.clientWidth / canvasContainer.value.clientHeight
    camera.updateProjectionMatrix()
    renderer.setSize(canvasContainer.value.clientWidth, canvasContainer.value.clientHeight)
  }
}

const activeSection = ref('about')

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id
        }
      })
    },
    { threshold: 0.5 },
  ) // 50% section terlihat baru dianggap aktif

  document.querySelectorAll('section[id]').forEach((section) => {
    observer.observe(section)
  })
})

// Panggil di Lifecycle Hooks
onMounted(() => {
  if (window.innerWidth > 768) {
    window.addEventListener('mousemove', updateCursor)
  } else {
    isDesktop.value = false
  }

  init3D() // Jalankan 3D
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  window.removeEventListener('mousemove', updateCursor)
  window.removeEventListener('resize', handleResize)
  cleanup3D() // Bersihkan RAM
})

onMounted(() => {
  if (window.innerWidth > 768) {
    window.addEventListener('mousemove', updateCursor)
  } else {
    isDesktop.value = false
  }
})

onUnmounted(() => {
  window.removeEventListener('mousemove', updateCursor)
})

const skills = ref([
  { name: 'Vue.js', icon: 'devicon-vuejs-plain colored' },
  { name: 'React.js', icon: 'devicon-react-original colored' },
  { name: 'JavaScript', icon: 'devicon-javascript-plain colored' },
  { name: 'Tailwind CSS', icon: 'devicon-tailwindcss-original colored' },
  { name: 'HTML5', icon: 'devicon-html5-plain colored' },
  { name: 'CSS3', icon: 'devicon-css3-plain colored' },
  { name: 'Python', icon: 'devicon-python-plain colored' },
  { name: 'Java', icon: 'devicon-java-plain colored' },
  { name: 'PHP', icon: 'devicon-php-plain colored' },
  { name: 'MySQL', icon: 'devicon-mysql-plain colored' },
  { name: 'Node.js', icon: 'devicon-nodejs-plain colored' },
  { name: 'Figma', icon: 'devicon-figma-plain colored' },
  { name: 'Machine Learning', icon: 'devicon-tensorflow-original colored' },
])

import diamondImg from '@/assets/diamond.png'
import icartradeImg from '@/assets/icartrade.png'
import cordialImg from '@/assets/cordial.png'
import signflowImg from '@/assets/signflow.png'

const projects = ref([
  {
    category: 'Final Thesis (2025)',
    name: 'SignFlow',
    image: signflowImg,
    github: 'https://github.com/christvann/SignFlow-Web',
    description:
      'A Web-Based Sign Language Detection System utilizing Convolutional Neural Networks (CNN) to translate sign language gestures accurately.',
    link: '#',
  },
  {
    category: 'Internship Project (2024)',
    name: 'Diamond (PLN Application)',
    image: diamondImg,
    github: 'https://github.com/christvann/Diamond_Application',
    description:
      'Internal enterprise application for PLN Icon Plus. Built and maintained 5+ core application pages including role-based interactive dashboards.',
    link: '#',
  },
  {
    category: 'Web Platform (2024)',
    name: 'ICarTrade Marketplace',
    image: icartradeImg,
    github: 'https://github.com/christvann/ICarTrade_Marketplace',
    description:
      'An online marketplace platform developed to streamline the buying and selling of automotive products with user profile management.',
    link: '#',
  },
  {
    category: 'UI/UX & Frontend (2024)',
    name: 'Cordial Crafts Shop',
    image: cordialImg,
    github: 'https://github.com/christvann/Cordial_Craft_Shop',
    description:
      'E-commerce interface focused on creating an aesthetically pleasing, user-friendly layout with high-quality imagery and intuitive navigation.',
    link: '#',
  },
])
// --- LOGIKA 3D CAROUSEL ---
const activeSlide = ref(1) // Set slide tengah (index 1) sebagai aktif pertama kali

const nextSlide = () => {
  activeSlide.value = (activeSlide.value + 1) % projects.value.length
}

const prevSlide = () => {
  activeSlide.value = (activeSlide.value - 1 + projects.value.length) % projects.value.length
}

const goToSlide = (index) => {
  activeSlide.value = index
}

// Fungsi untuk menentukan posisi 3D setiap kartu
const getCardClass = (index) => {
  if (index === activeSlide.value) return 'active'
  if (index === (activeSlide.value - 1 + projects.value.length) % projects.value.length)
    return 'prev'
  if (index === (activeSlide.value + 1) % projects.value.length) return 'next'
  return 'hidden' // Sembunyikan kartu yang tidak berada di dekat posisi aktif
}

const touchStartX = ref(0)
const touchEndX = ref(0)

// Fungsi saat jari mulai menyentuh layar
const handleTouchStart = (e) => {
  touchStartX.value = e.touches[0].clientX
}

// Fungsi saat jari dilepas dari layar
const handleTouchEnd = (e) => {
  touchEndX.value = e.changedTouches[0].clientX
  handleSwipeGesture()
}

// Logika penentu arah swipe
const handleSwipeGesture = () => {
  const swipeThreshold = 50 // Jarak minimal geser (dalam pixel) agar slide berpindah
  const difference = touchStartX.value - touchEndX.value

  if (Math.abs(difference) > swipeThreshold) {
    if (difference > 0) {
      // Geser ke kiri -> Slide selanjutnya
      nextSlide()
    } else {
      // Geser ke kanan -> Slide sebelumnya
      prevSlide()
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;800;900&display=swap');

html {
  scroll-behavior: smooth;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  background: rgba(3, 3, 3, 0.8); /* Transparan gelap */
  backdrop-filter: blur(10px); /* Efek kaca buram */
  z-index: 1000;
  display: flex;
  align-items: center;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.nav-container {
  max-width: 1400px;
  width: 90%;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* LOGO STYLE (Sesuai gambar kamu) */
.nav-logo {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-circle {
  width: 32px;
  height: 32px;
  border: 1.5px solid #e60000; /* Merah glow */
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 10px rgba(230, 0, 0, 0.3);
}

.logo-letter {
  color: #fff;
  font-weight: 800;
  font-size: 14px;
}

.logo-text {
  font-size: 1.2rem;
  font-weight: 800;
  color: #fff;
  letter-spacing: -0.5px;
}

/* NAVIGATION LINKS */
.nav-links {
  display: flex;
  gap: 40px;
}

.nav-item {
  color: #888;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
}

.nav-item:hover,
.nav-item.active {
  color: #fff;
}

/* Garis bawah tipis saat active/hover */
.nav-item::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: #e60000;
  transition: width 0.3s ease;
}

.nav-item:hover::after,
.nav-item.active::after {
  width: 100%;
}

/* Terapkan ke seluruh elemen tanpa terkecuali */
* {
  font-family: 'Inter', sans-serif !important;
}
/* Reset Global */
body {
  background-color: #030303;
  color: #ffffff;
  font-family: 'Inter', sans-serif;
  overflow-x: hidden;
  margin: 0;
  background-image: radial-gradient(circle at top right, rgba(230, 0, 0, 0.08), transparent 40%);
  background-attachment: fixed;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1,
h2,
h3,
.section-title {
  font-family: 'Inter', sans-serif;
  font-weight: 800; /* Sangat Tebal */
  letter-spacing: -0.02em; /* Sedikit dirapatkan agar terlihat modern */
  line-height: 1.1;
  margin-bottom: 20px;
}

/* Styling Deskripsi di bawah judul */
p,
.exp-desc-list,
.bio {
  font-family: 'Inter', sans-serif;
  font-weight: 400;
  line-height: 1.6;
  color: #aaaaaa; /* Warna abu-abu sesuai gambar */
  max-width: 800px; /* Agar tidak terlalu lebar dan enak dibaca */
}

.contact-section {
  position: relative;
  z-index: 5;
  margin-top: 150px;
  min-height: 80vh; /* Sesuaikan dengan kebutuhan tinggi konten */
  display: flex;
  flex-direction: column;
  align-items: center; /* Mengetengahkan konten secara horizontal */
  justify-content: space-between; /* Memberi ruang antara konten utama dan footer */
  width: 100%;
  background-color: #030303;
}

.contact-container {
  max-width: 1200px;
  width: 90%;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 80px;
  align-items: center;
}

/* KIRI: TYPOGRAPHY */
.contact-title {
  font-family: 'Inter', sans-serif;
  font-size: 6rem;
  font-weight: 900;
  line-height: 0.9;
  margin: 0;
  color: #fff;
  letter-spacing: -3px;
}

.contact-title .highlight {
  color: transparent;
  -webkit-text-stroke: 1.5px #e60000; /* Teks outline merah */
  transition: all 0.5s ease;
}

.contact-title:hover .highlight {
  color: #e60000;
  text-shadow: 0 0 30px rgba(230, 0, 0, 0.5);
}

.contact-subtitle {
  font-size: 1.1rem;
  color: #888;
  margin-top: 30px;
  line-height: 1.6;
}

.social-links {
  display: flex;
  gap: 25px;
  margin-top: 50px;
}

.social-item {
  color: #888; /* Warna default abu-abu agar tidak terlalu mencolok */
  font-size: 2.2rem; /* Ukuran ikon */
  text-decoration: none;
  transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
}

.instagram-svg svg {
  width: 35px;
  height: 35px;
  stroke: currentColor;
}

.social-item:hover {
  color: #e60000; /* Warna merah identitasmu */
  transform: translateY(-5px);
  filter: drop-shadow(0 0 12px rgba(230, 0, 0, 0.7));
}

.social-item i {
  line-height: 1;
}

/* KANAN: ACTION AREA */
.main-contact-btn {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #fff;
  color: #000;
  padding: 25px 35px;
  text-decoration: none;
  font-weight: 800;
  font-size: 1.2rem;
  border-radius: 5px;
  transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
  margin: 40px 0;
}

.main-contact-btn:hover {
  background: #e60000;
  color: #fff;
  transform: scale(1.02);
  box-shadow: 0 10px 40px rgba(230, 0, 0, 0.3);
}

.location-tag {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #fff;
  font-size: 0.9rem;
  opacity: 0.7;
}

.availability {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 0.9rem;
  color: #888;
}

.status-dot {
  width: 8px;
  height: 8px;
  background: #00ff00; /* Hijau menyala */
  border-radius: 50%;
  box-shadow: 0 0 10px #00ff00;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.5);
    opacity: 0.5;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.mini-footer {
  width: 100%;
  padding: 40px 0;
  display: flex;
  justify-content: center; /* Mengetengahkan konten di dalam footer */
  align-items: center;
  border-top: 1px solid rgba(255, 255, 255, 0.05); /* Garis tipis transparan */
  margin-top: auto; /* Memastikan footer selalu nempel di paling bawah section */
}

.mini-footer p {
  color: #444; /* Warna abu-abu redup agar tidak distraksi */
  font-size: 0.75rem;
  letter-spacing: 3px; /* Memberi kesan luas dan minimalis */
  text-transform: uppercase;
  margin: 0;
  font-weight: 300;
  opacity: 0.6;
}

/* Responsive */
@media (max-width: 968px) {
  .contact-container {
    grid-template-columns: 1fr;
    text-align: left;
    gap: 40px;
  }
  .contact-title {
    font-size: 4rem;
  }
}
</style>

<style scoped>
.project-3d-card {
  background: transparent !important;
  position: relative;
  overflow: hidden;
  border-radius: 20px;
  border: none !important;
  /* Pastikan kartu punya tinggi yang cukup */
  height: 450px;
  box-shadow: none;
}

/* Container Gambar di dalam Kartu */
.project-image-wrapper {
  grid-area: 1 / 1; /* Menempati sel yang sama dengan teks */
  width: 100%;
  height: 100%;
  z-index: 1;
}

.project-img-display {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.4);
  transition: all 0.7s ease;
}

/* Efek Hover: Gambar nge-zoom dikit */
.project-3d-card.active .project-img-display {
  filter: brightness(0.7);
  transform: scale(1.1);
}

/* Overlay halus agar gambar menyatu dengan tema dark */
.img-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* Gradient lebih gelap di bawah untuk readability teks */
  background: linear-gradient(
    to top,
    rgba(3, 3, 3, 1) 0%,
    /* Hitam pekat sesuai background web di bawah */ rgba(3, 3, 3, 0.5) 40%,
    /* Mulai transparan di tengah */ transparent 100% /* Benar-benar bening di atas gambar */
  );
  z-index: 2;
}

/* Penyesuaian konten agar rapi */
.project-content {
  background: transparent !important;
  position: relative;
  width: 100%;
  height: 450px; /* Pastikan tinggi ini sama dengan .project-3d-card */
  overflow: hidden;
  display: grid;
  place-items: stretch; /* Memastikan isi memenuhi grid */
}

.project-details-overlay {
  grid-area: 1 / 1;
  z-index: 3;
  display: flex;
  flex-direction: column;
  justify-content: flex-end; /* Teks tetap di bawah */

  padding: 30px 25px 40px 25px; /* Kurangi padding bawah (20px) agar ikon naik */

  background: transparent !important;
  border-radius: 15px;

  text-align: left;
  box-sizing: border-box;

  /* Animasi muncul (tetap sama) */
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.5s ease;
}

.project-3d-card.active .project-details-overlay {
  opacity: 1;
  transform: translateY(0);
}

.project-details {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.5s ease-out;
}

.project-name {
  font-family: 'Inter', sans-serif;
  font-weight: 900;
  font-size: 1.8rem;
  text-transform: uppercase;
  color: #fff;
  margin: 5px 0 5px 0; /* Kurangi margin bottom (5px) */
  letter-spacing: -1px;
}

.project-desc {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.8);

  /* --- PERBAIKAN: KURANGI MARGIN --- */
  margin-bottom: 10px; /* Jarak ke ikon GitHub (kurangi dari 15px) */

  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Membuat teks sedikit lebih terang saat kartu di-hover */
.project-3d-card.active .project-details {
  opacity: 1;
  transform: translateY(0);
  transition-delay: 0.3s;
}

.project-footer {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  /* Pastikan tidak ada margin-top di sini jika sudah ada margin-bottom di project-desc */
}

.github-icon-link {
  font-size: 1.8rem;
  color: #fff;
  transition: all 0.3s ease;
  display: inline-block;
  line-height: 1; /* Pastikan ikon tidak punya line-height tinggi */
}

/* Efek Hover Cyber-Noir */
.github-icon-link:hover {
  color: #e60000;
  filter: drop-shadow(0 0 15px #e60000);
  transform: scale(1.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
  position: relative;
  z-index: 2;
}

.cursor-glow {
  position: fixed;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(230, 0, 0, 0.05) 0%, transparent 50%);
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  z-index: 1;
}

.hero-section {
  min-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: space-between; /* Memisahkan teks ke kiri, 3D ke kanan */
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  gap: 2rem;
}

.hero-content {
  flex: 1; /* Teks mengambil sisa ruang */
  max-width: 600px;
}

/* Kontainer 3D baru kita */
.canvas-3d-container {
  width: 500px;
  height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  /* Tambahkan efek glow di belakang 3D-nya */
  background: radial-gradient(circle, rgba(230, 0, 0, 0.1) 0%, transparent 60%);
}

/* Penyesuaian responsif untuk layar HP */
@media (max-width: 768px) {
  .hero-section {
    flex-direction: column-reverse; /* Teks di bawah, 3D di atas saat di HP */
    text-align: center;
    justify-content: center;
  }
  .canvas-3d-container {
    width: 300px;
    height: 300px;
  }
}

.role-title {
  color: #e60000;
  font-size: 0.9rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 16px;
}

.main-name {
  font-size: 4.5rem;
  font-weight: 700;
  line-height: 1.1;
  margin-bottom: 24px;
}

.bio {
  color: #888888;
  font-size: 1.1rem;
  line-height: 1.7;
  max-width: 700px;
}

.section-title {
  font-size: 2rem;
  margin: 80px 0 40px;
  font-weight: 500;
}

.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}

.skills-section {
  /* TAMBAHKAN INI: Paksa jarak aman dari bagian Experience */
  margin-top: 60px;
  position: relative;
  z-index: 10;
}

.glow-card {
  display: flex;
  align-items: center;
  gap: 12px;
  background: rgba(20, 20, 20, 0.6);
  border: 1px solid rgba(230, 0, 0, 0.1);
  padding: 16px 32px;
  border-radius: 8px;
  font-weight: 500;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
  cursor: pointer;
}
.skill-icon {
  font-size: 1.8rem; /* Mengatur besar kecilnya logo */
}

.glow-card:hover {
  border-color: #e60000;
  box-shadow:
    0 0 20px rgba(230, 0, 0, 0.3),
    inset 0 0 10px rgba(230, 0, 0, 0.3);
  transform: translateY(-3px);
}

.carousel-container {
  display: flex;
  overflow-x: auto;
  gap: 24px;
  padding-bottom: 40px;
  scrollbar-width: none;
}
.carousel-container::-webkit-scrollbar {
  display: none;
}

.project-slide {
  min-width: 380px;
  background: linear-gradient(145deg, #111111, #0a0a0a);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 32px;
  display: flex;
  flex-direction: column;
  transition: transform 0.4s ease;
}

.project-slide:hover {
  transform: scale(0.98) rotateY(-5deg);
  border-color: rgba(230, 0, 0, 0.3);
}

.project-date {
  color: #888888;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 12px;
  display: block;
}

.project-name {
  font-size: 1.5rem;
  margin-bottom: 16px;
}

.project-desc {
  color: #888888;
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 32px;
  flex-grow: 1;
}

.see-more-btn {
  color: #e60000;
  text-decoration: none;
  font-weight: 700;
  font-size: 0.85rem;
  letter-spacing: 1px;
  display: inline-block;
  transition: text-shadow 0.3s ease;
}

.see-more-btn:hover {
  text-shadow: 0 0 10px #e60000;
}

@media (max-width: 768px) {
  .main-name {
    font-size: 3rem;
  }
  .project-slide {
    min-width: 300px;
  }
}

.carousel-3d-indicators {
  /* Memberi jarak yang jauh setelah indikator titik-titik sebelum masuk ke footer/contact */
  margin-top: 80px;
  margin-bottom: 100px;
}

/* --- 3D CAROUSEL STYLES --- */
.carousel-3d-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 100%;
  height: 500px; /* Sesuaikan tinggi carousel */
  perspective: 1200px; /* KUNCI 3D: Memberikan jarak pandang mata */
  margin-bottom: 20px;
  touch-action: pan-y;
  user-select: none;
  cursor: grab;
  user-select: none;
}

.carousel-3d-wrapper:active {
  cursor: grabbing; /* Tangan mengepal saat menekan */
}

.carousel-3d-container {
  position: relative;
  width: 350px;
  height: 450px;
  transform-style: preserve-3d;
}

/* Base Card Style */
.project-3d-card {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 500px;
  background: linear-gradient(145deg, #111111, #050505);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  padding: 32px;
  display: flex;
  flex-direction: column;
  transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1); /* Animasi transisi mulus */
  cursor: pointer;
  overflow: hidden;
}

/* Efek Glow Merah (Tersembunyi secara default) */
.card-glow-effect {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border-radius: 20px;
  box-shadow: 0 0 0 transparent;
  transition:
    box-shadow 0.4s ease,
    background 0.4s ease;
  pointer-events: none;
  z-index: 0;
}

.project-content {
  position: relative;
  z-index: 1; /* Pastikan teks di atas efek glow */
  height: 500px;
  display: flex;
  flex-direction: column;
  background: transparent !important;
}

/* Posisi 3D: Aktif (Di Tengah) */
.project-3d-card.active {
  box-shadow: 0 0 40px rgba(230, 0, 0, 0.25);
  transform: translateX(0) translateZ(0) rotateY(0);
  z-index: 10;
  opacity: 1;
  border: 1px solid rgba(230, 0, 0, 0.3);
  transition: all 0.5s ease;
}

/* Posisi 3D: Kartu Kiri */
.project-3d-card.prev {
  transform: translateX(-65%) translateZ(-150px) rotateY(25deg);
  z-index: 2;
  opacity: 0.5;
}

/* Posisi 3D: Kartu Kanan */
.project-3d-card.next {
  transform: translateX(65%) translateZ(-150px) rotateY(-25deg);
  z-index: 2;
  opacity: 0.5;
}

/* Posisi 3D: Tersembunyi */
.project-3d-card.hidden {
  transform: translateX(0) translateZ(-300px) rotateY(0);
  z-index: 1;
  opacity: 0;
  pointer-events: none;
}

/* --- HOVER EFFECT: NEON RED GLOW --- */
.project-3d-card.active:hover .card-glow-effect {
  /* Ini mereplikasi efek cahaya merah intens dari gambar referensimu */
  box-shadow:
    0 0 50px rgba(230, 0, 0, 0.5),
    inset 0 0 20px rgba(230, 0, 0, 0.2);
  background: radial-gradient(circle at center, rgba(230, 0, 0, 0.1) 0%, transparent 70%);
}

.project-3d-card.active:hover {
  border-color: #e60000;
}

/* Tombol Navigasi */
.nav-btn {
  background: rgba(20, 20, 20, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  z-index: 10;
  position: absolute;
  transition: all 0.3s;
  backdrop-filter: blur(5px);
}

.nav-btn:hover {
  background: #e60000;
  border-color: #e60000;
  box-shadow: 0 0 15px rgba(230, 0, 0, 0.5);
}

.nav-btn.prev {
  left: 10%;
}
.nav-btn.next {
  right: 10%;
}

/* Indikator Titik (Dots) */
.carousel-indicators {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 10px;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  cursor: pointer;
  transition: all 0.3s;
}

.dot.active {
  background: #e60000;
  box-shadow: 0 0 10px #e60000;
  transform: scale(1.3);
}

/* Responsif untuk Mobile */
@media (max-width: 768px) {
  .carousel-3d-container {
    width: 280px;
    height: 400px;
  }
  .project-3d-card {
    height: 400px; /* Perkecil sedikit di HP agar tidak terlalu penuh */
  }

  .project-3d-card.prev {
    transform: translateX(-40%) translateZ(-150px) rotateY(15deg);
  }
  .project-3d-card.next {
    transform: translateX(40%) translateZ(-150px) rotateY(-15deg);
  }
  .nav-btn {
    display: none;
  }

  .project-name {
    font-size: 1.4rem;
  }
}

/* --- EXPERIENCE & EDUCATION STYLES (3D GLOW CARDS) --- */
.experience-section {
  padding-top: 40px;
  margin-bottom: 80px;
}

.timeline-horizontal-wrapper {
  position: relative;
  width: 100%;
  margin-top: 40px;
}

/* Garis Laser Merah di Tengah */
.timeline-line-hz {
  position: absolute;
  top: 34px;
  left: 0;
  width: 100%;
  height: 2px;
  background: rgba(230, 0, 0, 0.08);
  z-index: 1;
}
.timeline-line-hz::before {
  content: '';
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: -250px;
  width: 300px;
  height: 3px;

  /* Gradient yang lebih terang di tengah sesuai permintaan */
  background: linear-gradient(90deg, transparent 0%, rgba(255, 30, 30, 0.9) 50%, transparent 100%);

  /* Cahaya yang lebih terang dan menyebar */
  box-shadow:
    0 0 20px rgba(230, 0, 0, 0.5),
    0 0 40px rgba(230, 0, 0, 0.2);

  animation: dustFlow 12s cubic-bezier(0.4, 0, 0.2, 1) infinite;
  filter: blur(1.5px);
}

@keyframes dustFlow {
  0% {
    left: -250px;
    opacity: 0;
  }
  20% {
    opacity: 0.6; /* Tidak terlalu terang, tetap redup */
  }
  80% {
    opacity: 0.6;
  }
  100% {
    left: 100%;
    opacity: 0;
  }
}

/* Kontainer untuk setiap item (Bagi 2 layar) */
.timeline-horizontal-container {
  display: flex;
  gap: 50px; /* Jarak antar kartu */
  overflow-x: auto;
  padding: 0 20px 80px 20px; /* Padding bawah ekstra untuk efek 3D tilt */
  scrollbar-width: none; /* Sembunyikan scrollbar di Firefox */
}
.timeline-horizontal-container::-webkit-scrollbar {
  display: none; /* Sembunyikan scrollbar di Chrome/Safari */
}

/* Posisi Kartu Genap (Kiri) */
.timeline-item-hz {
  position: relative;
  flex: 0 0 auto;
  width: 350px;
  padding-top: 100px; /* Berubah dari 50px menjadi 100px (Memberi ruang lega di atas kartu) */
}

/* Posisi Kartu Ganjil (Kanan) */
.timeline-item.right {
  left: 50%;
  justify-content: flex-start; /* Dorong kartu ke arah garis tengah */
}

/* Titik Indikator di Garis Tengah */
.timeline-dot-hz {
  position: absolute;
  top: 20px; /* Berubah dari 0 menjadi 20px */
  left: 50%;
  transform: translateX(-50%);
  width: 20px;
  height: 20px;
  background-color: #030303;
  border: 4px solid #e60000;
  border-radius: 50%;
  box-shadow: 0 0 15px rgba(230, 0, 0, 0.8);
  z-index: 2;
}

/* Penyesuaian letak titik berdasarkan sisi kiri/kanan */
.timeline-item.left .timeline-dot {
  right: -8px; /* Geser ke garis tengah */
}
.timeline-item.right .timeline-dot {
  left: -8px; /* Geser ke garis tengah */
}

/* --- RESPONSIVE MOBILE (Penting!) --- */
/* Di HP, timeline jangan berselang-seling agar kartu tidak terlalu kecil */
@media (max-width: 768px) {
  .timeline-line {
    left: 20px; /* Geser garis ke pinggir kiri */
  }

  .timeline-item {
    width: 100%;
    padding-left: 60px; /* Beri ruang untuk garis di kiri */
    padding-right: 0;
  }

  /* Semua kartu numpuk di sebelah kanan garis */
  .timeline-item.left,
  .timeline-item.right {
    left: 0;
    justify-content: flex-start;
  }

  /* Posisikan semua titik di garis sebelah kiri */
  .timeline-item.left .timeline-dot,
  .timeline-item.right .timeline-dot {
    left: 12px;
    right: auto;
  }
}
/* KUNCI 3D: Container yang memberikan perspektif jarak pandang */
.exp-card-container {
  perspective: 1000px;
  width: 340px;
}

/* Kartu Utama */
.exp-card {
  background: linear-gradient(145deg, #111111, #050505);
  border: 1px solid rgba(255, 26, 26, 0.05);
  border-radius: 16px;
  padding: 50px 30px 40px;
  position: relative;
  height: 100%;
  display: flex;
  flex-direction: column;
  /* KUNCI: Transisi cepat agar tidak delay dengan mouse, transform-style WAJIB ada */
  transition:
    transform 0.1s ease-out,
    box-shadow 0.3s ease,
    border-color 0.3s ease;
  transform-style: preserve-3d;
}

/* EFEK HOVER: Kartu miring dan bersinar (Ringan di Android!) */
.exp-card:hover {
  border-color: rgba(230, 0, 0, 0.5);
  box-shadow:
    0 15px 30px rgba(230, 0, 0, 0.2),
    inset 0 0 20px rgba(230, 0, 0, 0.05);
  z-index: 10;
}

/* Badge Kotak "June 29" ala referensi */
.date-badge {
  position: absolute;
  top: -25px; /* Menonjol ke luar batas atas kartu */
  left: 30px;
  background-color: #000000;
  border: 1px solid #e60000;
  box-shadow: 0 0 15px rgba(230, 0, 0, 0.3);
  padding: 10px 16px;
  border-radius: 8px;
  text-align: center;
  z-index: 2;
  transform: translateZ(20px); /* Efek pop-out 3D saat di-hover */
}

.badge-subtitle {
  display: block;
  font-size: 0.7rem;
  font-weight: 700;
  color: #888888;
  letter-spacing: 1px;
}

.badge-title {
  display: block;
  font-size: 1.2rem;
  font-weight: 900;
  color: #e60000;
}

/* Teks dalam kartu */
.exp-title {
  font-size: 1.4rem;
  margin-bottom: 16px;
  color: #ffffff;
}

.exp-desc-list {
  list-style: none;
  padding: 0;
  margin: 0 0 24px 0;
  font-size: 0.9rem;
  line-height: 1.6;
  color: #aaaaaa;
  text-align: left; /* Menjaga teks tetap rata kiri di dalam kartu */
}

.exp-desc-list li {
  position: relative;
  padding-left: 20px;
  margin-bottom: 10px;
}

/* Custom Dot Merah Neon */
.exp-desc-list li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 8px;
  width: 6px;
  height: 6px;
  background-color: #e60000;
  border-radius: 50%;
  box-shadow: 0 0 8px #ff0000;
}

/* Responsif Mobile */
@media (max-width: 768px) {
  .exp-card-container {
    width: 100%;
    max-width: 340px;
  }
  .exp-card:hover {
    transform: translateY(-5px);
  } /* Matikan tilt 3D di HP agar lebih mudah disentuh */
}
.parallax-item,
.parallax-item-low,
.parallax-item-high {
  transition: transform 0.3s ease-out;
}

/* Saat kartu disentuh mouse, dorong teks ke arah layar (translateZ) */
.exp-card:hover .parallax-item {
  transform: translateZ(30px); /* Teks biasa timbul 30px */
}

.exp-card:hover .parallax-item-low {
  transform: translateZ(20px); /* Tombol timbul sedikit (20px) */
}

.exp-card:hover .parallax-item-high {
  transform: translateZ(50px); /* Badge "GRAD 2024" paling menonjol (50px) */
}

/* Pastikan date-badge posisi default-nya mereset Z agar tidak berantakan */
.date-badge {
  position: absolute;
  top: -25px;
  left: 30px;
  background-color: #000000;
  border: 1px solid #e60000;
  box-shadow: 0 0 15px rgba(230, 0, 0, 0.3);
  padding: 10px 16px;
  border-radius: 8px;
  text-align: center;
}
</style>
