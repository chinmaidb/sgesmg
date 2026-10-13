<script setup>
import { computed, ref } from "vue";
import {
  ArrowDownRight,
  ArrowRight,
  ArrowUpRight,
  BadgeCheck,
  BriefcaseBusiness,
  CarFront,
  Check,
  ChevronDown,
  CircleHelp,
  Clock3,
  FileCheck2,
  Fingerprint,
  Laptop,
  Menu,
  MonitorCog,
  Printer,
  Search,
  ShieldCheck,
  Smartphone,
  Stamp,
  Ticket,
  Wrench,
  X,
  Zap,
} from "lucide-vue-next";

const menuOpen = ref(false);
const query = ref("");
const activeCategory = ref("All services");
const contactName = ref("");
const contactService = ref("E-Stamp & Documentation");
const contactMessage = ref("");
const showContactForm = ref(false);

const categories = [
  { name: "All services", count: "14+" },
  { name: "Government & documentation", count: "08" },
  { name: "Sales & technology", count: "03" },
  { name: "Repair & service", count: "03" },
];

const services = [
  {
    title: "E-Stamp & Documentation",
    category: "Government & documentation",
    desc: "E-stamp, lost PAN card number, passport assistance and marriage certificates.",
    icon: Stamp,
    tag: "DOCUMENTS",
    number: "01",
  },
  {
    title: "GST & Tax Returns",
    category: "Government & documentation",
    desc: "GST registration, income tax returns and VAT-related assistance.",
    icon: FileCheck2,
    tag: "TAX & COMPLIANCE",
    number: "02",
  },
  {
    title: "Insurance & LIC",
    category: "Government & documentation",
    desc: "Two-wheeler and four-wheeler insurance, plus LIC policy services.",
    icon: ShieldCheck,
    tag: "COVER & PROTECT",
    number: "03",
  },
  {
    title: "RTO & Vehicle Works",
    category: "Government & documentation",
    desc: "Support for a wide range of RTO-related services and paperwork.",
    icon: CarFront,
    tag: "MOBILITY",
    number: "04",
  },
  {
    title: "Business Registrations",
    category: "Government & documentation",
    desc: "Shop registration, food licence and other essential registrations.",
    icon: BriefcaseBusiness,
    tag: "BUSINESS",
    number: "05",
  },
  {
    title: "Railway Tickets & PF",
    category: "Government & documentation",
    desc: "Railway ticket assistance and PF withdrawal support.",
    icon: Ticket,
    tag: "EVERYDAY SERVICES",
    number: "06",
  },
  {
    title: "Computers & Laptops",
    category: "Sales & technology",
    desc: "New and used laptops, desktop PCs and computer essentials.",
    icon: Laptop,
    tag: "SHOP TECH",
    number: "07",
  },
  {
    title: "Accessories & Devices",
    category: "Sales & technology",
    desc: "Computer, mobile and printer accessories, plus networking devices.",
    icon: Smartphone,
    tag: "GEAR UP",
    number: "08",
  },
  {
    title: "Laptop & PC Repair",
    category: "Repair & service",
    desc: "Troubleshooting, maintenance and repairs for laptops and desktop PCs.",
    icon: MonitorCog,
    tag: "TECH SUPPORT",
    number: "09",
  },
  {
    title: "Printer Service",
    category: "Repair & service",
    desc: "Printer diagnostics and service support to get you back to work.",
    icon: Printer,
    tag: "PRINT BETTER",
    number: "10",
  },
  {
    title: "Mobile & More",
    category: "Repair & service",
    desc: "Mobile service and additional technology support. Ask us about your need.",
    icon: Wrench,
    tag: "FIX & RESTORE",
    number: "11",
  },
];

const filteredServices = computed(() => {
  const needle = query.value.trim().toLowerCase();
  return services.filter((service) => {
    const categoryMatch =
      activeCategory.value === "All services" ||
      service.category === activeCategory.value;
    const searchMatch =
      !needle ||
      `${service.title} ${service.desc} ${service.tag}`
        .toLowerCase()
        .includes(needle);
    return categoryMatch && searchMatch;
  });
});

function askAbout(service) {
  contactService.value = service;
  showContactForm.value = true;
  menuOpen.value = false;
  document.getElementById("contact")?.scrollIntoView({ behavior: "smooth" });
}

function submitInquiry() {
  const text = `Hello Shree Guru Enterprises!%0AName: ${encodeURIComponent(contactName.value || "Not provided")}%0AService: ${encodeURIComponent(contactService.value)}%0AMessage: ${encodeURIComponent(contactMessage.value || "I would like more information.")}`;
  // Replace this placeholder with the business's verified WhatsApp number.
  window.open(`https://wa.me/?text=${text}`, "_blank", "noopener,noreferrer");
}
</script>

<template>
  <div class="site-shell">
    <div class="topline">
      <span class="status-dot"></span>
      <span>YOUR LOCAL SERVICE & TECHNOLOGY DESK</span>
      <span class="topline-right"
        >EST. TO MAKE THINGS EASIER <span class="topline-star">✳</span></span
      >
    </div>

    <header class="site-header">
      <a href="#" class="brand" aria-label="Shree Guru Enterprises home">
        <span class="brand-mark"><span>SG</span><i></i></span>
        <span class="brand-copy"
          ><strong>SHREE GURU</strong
          ><small>ENTERPRISES / SERVICE STATION</small></span
        >
      </a>
      <nav class="desktop-nav" aria-label="Main navigation">
        <a href="#services">Services <span>01</span></a>
        <a href="#about">Our approach <span>02</span></a>
        <a href="#contact">Contact <span>03</span></a>
      </nav>
      <a class="header-cta" href="#contact"
        >LET'S TALK <ArrowUpRight :size="16"
      /></a>
      <button
        class="mobile-menu"
        @click="menuOpen = !menuOpen"
        :aria-label="menuOpen ? 'Close menu' : 'Open menu'"
      >
        <X v-if="menuOpen" :size="22" /><Menu v-else :size="22" />
      </button>
    </header>
    <div v-if="menuOpen" class="mobile-nav">
      <a href="#services" @click="menuOpen = false">Services</a>
      <a href="#about" @click="menuOpen = false">Our approach</a>
      <a href="#contact" @click="menuOpen = false">Contact</a>
    </div>

    <main>
      <section class="hero">
        <div class="hero-grid"></div>
        <div class="hero-content">
          <div class="eyebrow">
            <span class="eyebrow-line"></span> ONE DESK. MANY SOLUTIONS.
            <span class="eyebrow-code">[ SGE—001 ]</span>
          </div>
          <h1>
            Life's admin.<br /><span class="headline-accent">Handled.</span>
            Tech,<br />back in action.
          </h1>
          <p class="hero-lede">
            Welcome to Shree Guru Enterprises — your neighbourhood partner for
            essential documentation, registrations, insurance, technology sales
            and repairs.
          </p>
          <div class="hero-actions">
            <a class="button-primary" href="#services"
              >EXPLORE SERVICES <ArrowDownRight :size="17"
            /></a>
            <a class="button-text" href="#contact"
              >Tell us what you need <ArrowRight :size="16"
            /></a>
          </div>
          <div class="hero-footnote">
            <span class="tiny-cross">✳</span> PRACTICAL HELP. STRAIGHTFORWARD
            SERVICE.
          </div>
        </div>

        <div
          class="hero-art"
          aria-label="Decorative retro-futuristic illustration"
        >
          <div class="orbit orbit-one"></div>
          <div class="orbit orbit-two"></div>
          <div class="orbit orbit-three"></div>
          <div class="sun-disc"></div>
          <div class="art-grid"></div>
          <div class="floating-card card-stamp">
            <Stamp :size="20" /><span>E-STAMP</span
            ><small>DOCUMENTS / 01</small>
          </div>
          <div class="floating-card card-tech">
            <Laptop :size="22" /><span>TECH CARE</span
            ><small>REPAIR / 02</small>
          </div>
          <div class="hero-center-icon">
            <Zap :size="48" stroke-width="1.3" />
          </div>
          <div class="art-caption">
            <span>FIG. 01</span><span>THE EVERYDAY<br />PROBLEM SOLVER</span>
          </div>
          <div class="art-side-label">SERVICE / SYSTEM / SUPPORT</div>
        </div>
        <div class="hero-index">
          <span>01</span><span class="index-rule"></span><span>WELCOME</span>
        </div>
      </section>

      <section class="ticker" aria-label="Service highlights">
        <div class="ticker-track">
          <span>DOCUMENTATION <i>✳</i></span
          ><span>GOVERNMENT SERVICES <i>✳</i></span
          ><span>TECH SALES <i>✳</i></span
          ><span>REPAIRS & SUPPORT <i>✳</i></span
          ><span>DOCUMENTATION <i>✳</i></span
          ><span>GOVERNMENT SERVICES <i>✳</i></span>
        </div>
      </section>

      <section id="services" class="services-section section-pad">
        <div class="section-heading">
          <div>
            <div class="eyebrow dark-eyebrow">
              <span class="eyebrow-line"></span> THE SERVICE DIRECTORY / 001
            </div>
            <h2>
              What can we<br /><span class="text-outline">help you with?</span>
            </h2>
          </div>
          <p>
            From paperwork to hardware, find the support you need — all in one
            familiar place.
          </p>
        </div>

        <div class="service-tools">
          <div
            class="category-tabs"
            role="group"
            aria-label="Filter services by category"
          >
            <button
              v-for="category in categories"
              :key="category.name"
              @click="activeCategory = category.name"
              :class="{ active: activeCategory === category.name }"
            >
              {{ category.name }} <span>{{ category.count }}</span>
            </button>
          </div>
          <label class="search-box"
            ><Search :size="17" /><input
              v-model="query"
              type="search"
              placeholder="Find a service..."
              aria-label="Search services"
            /><span>/</span></label
          >
        </div>

        <div class="service-grid">
          <article
            v-for="service in filteredServices"
            :key="service.number"
            class="service-card"
          >
            <div class="card-top">
              <span class="service-number">{{ service.number }} / 11</span
              ><component
                :is="service.icon"
                :size="21"
                stroke-width="1.6"
                class="service-icon"
              />
            </div>
            <div class="service-tag">{{ service.tag }}</div>
            <h3>{{ service.title }}</h3>
            <p>{{ service.desc }}</p>
            <button class="card-link" @click="askAbout(service.title)">
              ASK ABOUT THIS <ArrowUpRight :size="16" />
            </button>
          </article>
          <div v-if="filteredServices.length === 0" class="no-results">
            <CircleHelp :size="25" />
            <h3>No matching services</h3>
            <p>Try a different keyword or choose another category.</p>
            <button
              class="button-primary"
              @click="
                query = '';
                activeCategory = 'All services';
              "
            >
              RESET FILTERS
            </button>
          </div>
        </div>
        <div class="directory-foot">
          <span
            >SHOWING
            {{ filteredServices.length.toString().padStart(2, "0") }}
            SERVICES</span
          ><span
            >MORE HELP?
            <a href="#contact">TALK TO OUR TEAM <ArrowUpRight :size="13" /></a
          ></span>
        </div>
      </section>

      <section id="about" class="promise-section">
        <div class="promise-left">
          <div class="eyebrow">
            <span class="eyebrow-line"></span> WHY SHREE GURU / 002
          </div>
          <h2>
            Less running<br />around. <span>More<br />getting done.</span>
          </h2>
          <p>
            Some tasks are complicated enough already. We bring everyday
            services and practical tech support together, so you can start with
            one conversation.
          </p>
          <a href="#contact" class="button-light"
            >LET'S GET STARTED <ArrowUpRight :size="16"
          /></a>
        </div>
        <div class="promise-right">
          <div class="promise-graphic">
            <div class="promise-circle">
              <BadgeCheck :size="54" stroke-width="1.1" /><span
                >HELPFUL BY DESIGN</span
              >
            </div>
            <div class="promise-cross">✳</div>
            <div class="promise-ring-label">
              LOCAL SUPPORT • PRACTICAL SOLUTIONS • LOCAL SUPPORT •
            </div>
          </div>
          <div class="promise-points">
            <div>
              <span>01</span>
              <div>
                <h3>A broad range, one stop</h3>
                <p>Documentation, registrations, sales and repair services.</p>
              </div>
              <Check :size="18" />
            </div>
            <div>
              <span>02</span>
              <div>
                <h3>Clear, practical guidance</h3>
                <p>
                  Tell us what you need and we'll help you understand the next
                  step.
                </p>
              </div>
              <Check :size="18" />
            </div>
            <div>
              <span>03</span>
              <div>
                <h3>Support beyond the sale</h3>
                <p>Tech products and service support for everyday devices.</p>
              </div>
              <Check :size="18" />
            </div>
          </div>
        </div>
      </section>

      <section class="process-strip">
        <div class="process-intro">
          <span class="eyebrow dark-eyebrow">THE EASY WAY / 003</span>
          <h2>Three steps.<br />One less headache.</h2>
        </div>
        <div class="process-step">
          <span>01</span>
          <div>
            <Fingerprint :size="25" />
            <h3>Tell us</h3>
            <p>Share the service or device you need help with.</p>
          </div>
        </div>
        <div class="process-step">
          <span>02</span>
          <div>
            <CircleHelp :size="25" />
            <h3>Get guidance</h3>
            <p>We'll explain the available options and next steps.</p>
          </div>
        </div>
        <div class="process-step">
          <span>03</span>
          <div>
            <Check :size="25" />
            <h3>Move forward</h3>
            <p>Get the support you came in for.</p>
          </div>
        </div>
      </section>

      <section id="contact" class="contact-section section-pad">
        <div class="contact-copy">
          <div class="eyebrow dark-eyebrow">
            <span class="eyebrow-line"></span> YOUR NEXT STEP / 004
          </div>
          <h2>Let's sort<br /><span>it out.</span></h2>
          <p>
            Have a question about a service, a device to repair, or looking for
            a laptop? Tell us what you need.
          </p>
          <div class="contact-detail">
            <span class="contact-icon"><Clock3 :size="19" /></span>
            <div>
              <strong>VISIT OR GET IN TOUCH</strong>
              <p>
                Contact us for current timings, availability and service
                details.
              </p>
            </div>
          </div>
          <div class="contact-detail">
            <span class="contact-icon"><CircleHelp :size="19" /></span>
            <div>
              <strong>NOT SURE WHICH SERVICE?</strong>
              <p>Choose “General enquiry” and describe what you need.</p>
            </div>
          </div>
        </div>
        <form class="contact-form" @submit.prevent="submitInquiry">
          <div class="form-top">
            <span>ENQUIRY FORM</span><span>SGE / CONTACT</span>
          </div>
          <label
            >Your name <span>OPTIONAL</span
            ><input
              v-model="contactName"
              type="text"
              placeholder="How should we address you?"
          /></label>
          <label
            >What do you need help with? <span>REQUIRED</span>
            <div class="select-wrap">
              <select v-model="contactService" required>
                <option>E-Stamp & Documentation</option>
                <option>GST & Tax Returns</option>
                <option>Insurance & LIC</option>
                <option>RTO & Vehicle Works</option>
                <option>Business Registrations</option>
                <option>Railway Tickets & PF</option>
                <option>Computers & Laptops</option>
                <option>Accessories & Devices</option>
                <option>Laptop & PC Repair</option>
                <option>Printer Service</option>
                <option>Mobile & More</option>
                <option>General enquiry</option></select
              ><ChevronDown :size="16" />
            </div>
          </label>
          <label
            >Anything else we should know? <span>OPTIONAL</span
            ><textarea
              v-model="contactMessage"
              rows="3"
              placeholder="A short note about your requirement..."
            ></textarea>
          </label>
          <button type="submit" class="button-primary submit-button">
            CONTINUE ON WHATSAPP <ArrowUpRight :size="17" />
          </button>
          <p class="form-note">
            This opens WhatsApp with your enquiry pre-filled. No message is sent
            automatically.
          </p>
        </form>
      </section>
    </main>

    <footer class="site-footer">
      <a href="#" class="brand footer-brand"
        ><span class="brand-mark"><span>SG</span><i></i></span
        ><span class="brand-copy"
          ><strong>SHREE GURU</strong
          ><small>ENTERPRISES / SERVICE STATION</small></span
        ></a
      >
      <p>
        Essential services. Everyday technology.<br />A little less complicated.
      </p>
      <a href="#" class="back-top">BACK TO TOP ↑</a>
      <div class="footer-bottom">
        <span>© {{ new Date().getFullYear() }} SHREE GURU ENTERPRISES</span
        ><span
          >BUILT BY
          <a
            href="https://chinmaidb.github.io/portfolio-v1/"
            class="font-bold text-lg"
            >chinmaidb</a
          ></span
        ><span
          >WITH
          <a href="https://shreshtasmg.in" class="font-bold text-sm"
            >shreshtasmg.in</a
          >
          <i>✳</i></span
        >
      </div>
    </footer>
  </div>
</template>
