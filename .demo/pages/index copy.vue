<template>
  <div class="container">
    <!-- Navbar -->
    <nav class="custom-navbar">
      <div class="custom-container">
        <!-- Brand Name -->
        <NuxtLink class="custom-navbar-brand" to="/">BrandName</NuxtLink>

        <!-- Toggler for responsive navbar -->
        <button class="custom-navbar-toggler" type="button" @click="toggleNavbar">
          <span class="custom-navbar-toggler-icon"></span>
        </button>

        <!-- Navbar Links -->
        <div :class="['custom-navbar-collapse', { 'show': isNavbarOpen }]" id="customNavbarNav">
          <ul class="custom-navbar-nav">
            <li class="custom-nav-item">
              <NuxtLink class="custom-nav-link" to="/">Home</NuxtLink>
            </li>
            <li class="custom-nav-item">
              <NuxtLink class="custom-nav-link" to="/about">About</NuxtLink>
            </li>
            <li class="custom-nav-item">
              <NuxtLink class="custom-nav-link" to="/services">Services</NuxtLink>
            </li>
            <li class="custom-nav-item">
              <NuxtLink class="custom-nav-link" to="/contact">Contact</NuxtLink>
            </li>
            <li class="custom-nav-item">
              <NuxtLink class="custom-nav-link" to="/auth">Login</NuxtLink>
            </li>
            <li class="custom-nav-item">
              <NuxtLink class="custom-nav-link" to="/auth">Signup</NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Header Section -->
    <header class="mt-3">
      <div class="row w-100">
        <!-- Column 1 -->
        <div class="col-md-4 d-flex flex-column justify-content-center align-items-center header-content">
          <div>
            <h1><b>Your<br>Perfect<br>Hairstyle<br>Awaits</b></h1>
            <p>Book an appointment with our expert</p>
          </div>
        </div>

        <!-- Column 2 -->
        <div class="col-md-8 d-flex justify-content-center align-items-center header-image">
          <img src="/custom/img/header.png" alt="Hair Salon" class="img-fluid">
        </div>
      </div>
    </header>


    <div class="services my-5">
      <h1><b>Book Your Appointment Online</b></h1>
      <p>Convenient and hassle-free booking system for your next hair appointment.</p>
    </div>




    <!-- =============== wizard =================================== -->
    <div class="grid w-full gap-10 md:grid-cols-12">
      <div class="md:col-span-3 lg:col-span-4">
        <div class="xs:w-full xs:max-w-xs xs:mx-auto flex flex-col gap-4 md:flex-row">
          <div class="xs:max-w-xs xs:mx-auto relative flex justify-between gap-7 md:flex-col">
            <!-- Progress Bar -->
            <div
              class="xs:top-1.5 xs:inset-x-0 bg-muted-200 dark:bg-muted-700 absolute start-2 top-2 z-0 mx-auto h-1 w-[calc(100%_-_1rem)] md:h-[calc(100%_-_1rem)] md:w-1 md:-translate-x-1/2"
            ></div>
            <div
              class="bg-primary-500 absolute start-2 top-0 z-10 mx-auto hidden w-0.5 -translate-x-1/2 rounded-full transition-all duration-300 md:block"
              :style="{ height: progressHeight + '%' }"
            ></div>
            <div
              class="bg-primary-500 absolute start-1.5 top-[7px] z-10 h-0.5 rounded-full transition-all duration-300 md:hidden"
              :style="{ width: progressWidth }"
            ></div>
            <!-- Steps Indicator -->
            <div
              v-for="index in totalSteps"
              :key="index"
              class="bg-muted-200 dark:bg-muted-700 relative z-20 flex size-4 items-center justify-center rounded-full"
            >
              <span
                :class="['scale-0', { 'scale-1': index <= currentStep }]"
                class="bg-primary-500 block size-2 rounded-full transition-transform duration-300"
              ></span>
            </div>
          </div>
          <div class="relative flex justify-center gap-7 md:flex-col md:justify-between">
            <!-- Step Labels -->
            <a v-for="(label, index) in labels" :key="index" role="button" tabindex="0" class="cursor-default h-4 leading-none">
              <span :class="{'text-muted-800 dark:text-muted-100': index + 1 === currentStep, 'text-muted-400 dark:text-muted-500': index + 1 !== currentStep}"
                class="font-heading block text-xs"
              >
                {{ label }}
              </span>
            </a>
          </div>
        </div>
      </div>
      <div class="md:col-span-9 lg:col-span-8">
        <form @submit.prevent="handleSubmit">
          <div class="w-full">
            <div class="mb-8 space-y-2">
              <h2 class="nui-heading nui-heading-2xl nui-weight-medium nui-lead-normal md:!3xl text-muted-800 dark:text-white">
                What do you want?
              </h2>
              <p class="nui-paragraph nui-paragraph-sm nui-weight-normal nui-lead-normal text-muted-500 dark:text-muted-400 max-w-sm">
                Choose a service under
              </p>
            </div>
            <div class="relative max-w-md space-y-3">
              <!-- Step Content -->
              <div v-show="currentStep === 1">
                <div class="nui-input-wrapper nui-input-default nui-input-md nui-input-rounded-sm nui-has-icon">
                  <input
                    type="text"
                    class="nui-input !p-4 !ps-12 !h-12"
                    placeholder="Ex: Service Name"
                    v-model="step1Data"
                  />
                  <div class="!h-12 !w-12 nui-input-icon">
                    <!-- Icon SVG -->
                  </div>
                </div>
              </div>
              <div v-show="currentStep === 2">
                <div class="nui-input-wrapper nui-input-default nui-input-md nui-input-rounded-sm nui-has-icon">
                  <input
                    type="text"
                    class="nui-input !p-4 !ps-12 !h-12"
                    placeholder="Ex: Recipient Name"
                    v-model="step2Data"
                  />
                  <div class="!h-12 !w-12 nui-input-icon">
                    <!-- Icon SVG -->
                  </div>
                </div>
              </div>
              <div v-show="currentStep === 3">
                <div class="nui-input-wrapper nui-input-default nui-input-md nui-input-rounded-sm nui-has-icon">
                  <input
                    type="text"
                    class="nui-input !p-4 !ps-12 !h-12"
                    placeholder="Ex: Recipient Address"
                    v-model="step3Data"
                  />
                  <div class="!h-12 !w-12 nui-input-icon">
                    <!-- Icon SVG -->
                  </div>
                </div>
              </div>
              <div v-show="currentStep === 4">
                <div class="nui-input-wrapper nui-input-default nui-input-md nui-input-rounded-sm nui-has-icon">
                  <input
                    type="number"
                    class="nui-input !p-4 !ps-12 !h-12"
                    placeholder="Ex: Amount"
                    v-model="step4Data"
                  />
                  <div class="!h-12 !w-12 nui-input-icon">
                    <!-- Icon SVG -->
                  </div>
                </div>
              </div>
              <div v-show="currentStep === 5">
                <div class="nui-input-wrapper nui-input-default nui-input-md nui-input-rounded-sm nui-has-icon">
                  <textarea
                    class="nui-input !p-4 !ps-12 !h-12"
                    placeholder="Review details"
                    v-model="step5Data"
                  ></textarea>
                  <div class="!h-12 !w-12 nui-input-icon">
                    <!-- Icon SVG -->
                  </div>
                </div>
              </div>
              <!-- Navigation Buttons -->
              <div class="flex gap-2">
                <button
                  v-if="currentStep < totalSteps"
                  type="button"
                  @click="handleContinue"
                  class="nui-button nui-button-lg nui-button-rounded-sm nui-button-solid nui-button-primary w-full"
                >
                  <span>Continue</span>
                </button>
                <button
                  v-if="currentStep === totalSteps"
                  type="submit"
                  class="nui-button nui-button-lg nui-button-rounded-sm nui-button-solid nui-button-primary w-full"
                >
                  <span>Submit</span>
                </button>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>

    <!-- =========================== wizard ======================================== -->


    <!-- Testimonial -->
    <div class="text-center main-testimonial my-5">
      <h1 class="my-5"><b>What People Say About Us</b></h1>
      <div class="row">
        <!-- Testimonial 1 -->
        <div class="col-md-4">
          <div class="testimonial">
            <div class="testimonial-text ml-5">
              <blockquote class="blockquote">
                <p class="mb-0">“I love the service at this hair salon. The staff is friendly and I always leave
                  feeling happy with my new hairdo.”</p>
              </blockquote>
              <div>
                <img src="/custom/img/DSC_0001.JPG" alt="Person" class="testimonial-img">
              </div>
              <div class="mx-3 mt-1">
                <span style="color: blue;"><b>M Zada</b></span>
                <br>
                <cite title="Source Title">Regular Customer</cite>
              </div>
            </div>
          </div>
        </div>

        <!-- Testimonial 2 -->
        <div class="col-md-4">
          <div class="testimonial">
            <div class="testimonial-text ml-5">
              <blockquote class="blockquote">
                <p class="mb-0">“I was hesitant to try a new salon, but I'm so glad I did. The stylists here are
                  talented and the atmosphere is welcoming.”</p>
              </blockquote>
              <div>
                <img src="/custom/img/DSC_0005.JPG" alt="Person" class="testimonial-img">
              </div>
              <div class="mx-3 mt-1">
                <span style="color: blue;"><b>M Ijaz</b></span>
                <br>
                <cite title="Source Title">Regular Customer</cite>
              </div>
            </div>
          </div>
        </div>

        <!-- Testimonial 3 -->
        <div class="col-md-4">
          <div class="testimonial">
            <div class="testimonial-text ml-5">
              <blockquote class="blockquote">
                <p class="mb-0">“I've been coming to this salon for years and it never disappoints. The quality
                  of service is consistently excellent.”</p>
              </blockquote>
              <div>
                <img src="/custom/img/DSC_0006.JPG" alt="Person" class="testimonial-img">
              </div>
              <div class="mx-3 mt-1">
                <span style="color: blue;"><b>Saud Zada</b></span>
                <br>
                <cite title="Source Title">Regular Customer</cite>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Accordion -->
    <div class="accordion my-5">
      <div v-for="(item, index) in items" :key="index" class="accordion-item">
        <h2 class="accordion-header">
          <button class="accordion-button" @click="toggle(index)" :class="{ active: activeIndex === index }">
            {{ item.header }}
          </button>
        </h2>
        <div class="accordion-body" v-show="activeIndex === index">
          <p v-html="item.body"></p>
        </div>
      </div>
    </div>


    <!-- acciordian of theme  -->
    <div class="md:max-w-lg">
      <BaseAccordion
        :items="accordion"
        exclusive
        action="chevron"
      />
    </div>



    <div class="">
      <br><br><br><br>
      <br><br><br><br>
    </div>
  </div>
</template>

<script setup>
import { useHead } from '#app'
import { definePageMeta } from '#imports' // Ensure this import is correct for Nuxt 3

// Set page meta and head elements
useHead({
  title: 'mindboost',
  meta: [
    // { name: 'theme-color', content: '#E9C046' }
  ],
  link: [
    { rel: 'stylesheet', href: 'https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css' }
  ],
  script: [
    { src: 'https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js' }
  ]
})

definePageMeta({
  layout: '/custom'
})

import { ref } from 'vue';

const isNavbarOpen = ref(false);

function toggleNavbar() {
  isNavbarOpen.value = !isNavbarOpen.value;
}


// customer 

// Define the items for the accordion
const items = ref([
  {
    header: 'What are the opening hours?',
    body: 'Our salon is open <strong>9:00 AM TO 6:00 PM</strong>, Monday to Saturday.',
  },
  {
    header: 'How do I book an appointment?',
    body: 'This is the second <strong>item\'s accordion body.</strong> It is hidden by default, until the collapse plugin adds the appropriate classes that we use to style each element.',
  },
  {
    header: 'Do you offer hairstyle services for special occasions?',
    body: 'This is the third item\'s accordion body. <strong>Saud Ur Rehman</strong> It is hidden by default, until the collapse plugin adds the appropriate classes that we use to style each element. These classes control the overall appearance.',
  },
]);

// State to track which accordion item is open
const activeIndex = ref(null);

// Toggle function to show/hide the accordion body
function toggle(index) {
  activeIndex.value = activeIndex.value === index ? null : index;
}



//  ===================================== datab ================================
import { computed } from 'vue';

const currentStep = ref(1);
const step1Data = ref('');
const step2Data = ref('');
const step3Data = ref('');
const step4Data = ref('');
const step5Data = ref('');
const totalSteps = 5; // Number of steps in the wizard

const progressHeight = computed(() => (currentStep.value / totalSteps) * 100);
const progressWidth = computed(() => `${(currentStep.value / totalSteps) * 100}%`);

const labels = ['Services', 'Recipient details', 'Recipient address', 'Amount', 'Review'];

function handleContinue() {
  if (currentStep.value < totalSteps) {
    currentStep.value++;
  }
}

// function handleSubmit() {
//   // Handle form submission
//   console.log('Form submitted', { step1Data, step2Data, step3Data, step4Data, step5Data });
// }

function handleSubmit() {
  // Prepare the data payload
  const payload = {
    step1Data: step1Data.value,
    step2Data: step2Data.value,
    step3Data: step3Data.value,
    step4Data: step4Data.value,
    step5Data: step5Data.value
  };

  // Send the data using fetch
  fetch('/api/booking', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(payload)
  })
  .then(response => response.json())
  .then(data => {
    console.log('Success:', data);
    // Handle the response data (e.g., navigate to a confirmation page)
  })
  .catch((error) => {
    console.error('Error:', error);
    // Handle the error (e.g., display an error message)
  });
}

</script>

<style scoped>
/* ============================ Add your styles here ============================ */
.testimonial-img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
  display: block;
  /* Ensures image is treated as a block element */
  margin: 0 auto;
  /* Centers the image horizontally */
}

.testimonial {
  display: flex;
  align-items: flex-start;
  margin-bottom: 1rem;
  text-align: center;
  /* Centers text inside the testimonial */
}

.testimonial-text {
  margin-left: 10px;
}

.main-testimonial {
  margin-top: 10rem;
}

#accordionPanelsStayOpenExample {
  margin-top: 7rem;
}

.services {
  margin-top: 7rem;
}


/* ============================ navbar style  ============================*/


.custom-navbar {
  padding: 1rem;
}

.custom-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.custom-navbar-brand {
  text-decoration: none;
  font-size: 1.5rem;
}

.custom-navbar-toggler {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  display: none;
  /* Hide by default */
}

.custom-navbar-toggler-icon::before {
  content: '☰';
  /* Use any icon here */
}

.custom-navbar-collapse {
  display: flex;
  flex-direction: row;
  /* Horizontal layout by default */
}

.custom-navbar-nav {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  /* Ensure items are horizontally aligned */
}

.custom-nav-item {
  margin-left: 1rem;
}

.custom-nav-link {
  text-decoration: none;
}

/* Mobile Styles */
@media (max-width: 768px) {
  .custom-navbar-toggler {
    display: block;
    /* Show on mobile */
  }

  .custom-navbar-collapse {
    display: none;
    flex-direction: column;
    /* Vertical layout on mobile */
    position: absolute;
    top: 60px;
    left: 0;
    width: 100%;
    background-color: #fff;
    /* Optional, for better visibility */
  }

  .custom-navbar-collapse.show {
    display: flex;
  }

  .custom-navbar-nav {
    flex-direction: column;
    /* Stack items vertically on mobile */
  }

  .custom-nav-item {
    margin: 0;
    padding: 1rem;
    border-bottom: 1px solid #ddd;
    /* Optional, for better separation */
  }
}


/*============================  Caresol Style ============================*/


.accordion {
  border: 1px solid #ddd;
  border-radius: 5px;
  overflow: hidden;
  width: 100%;
  max-width: 100%;
  margin: auto;
}

.accordion-item {
  border-bottom: 1px solid #ddd;
}

.accordion-header {
  margin: 0;
}

.accordion-button {
  background-color: #f8f9fa;
  color: #000;
  /* Text color for the header */
  border: none;
  width: 100%;
  padding: 15px;
  text-align: left;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  outline: none;
}

.accordion-button.active {
  background-color: #e9ecef;
}

.accordion-body {
  padding: 15px;
  background-color: #f1f1f1;
}



header {
  width: 100%;
}



.header-content h1 {
  font-size: 3rem;
  /* Adjust the font size as needed */
  line-height: 1.2;
  /* Adjust line height for better spacing */
  margin: 0;
}

h1 {
  font-size: 2.6rem;
  /* Adjust the font size as needed */
  line-height: 1.2;
  /* Adjust line height for better spacing */
  margin: 0;
}



.header-content p {
  font-size: 1.25rem;
  /* Adjust the font size for the paragraph */
  margin-top: 0.5rem;
}

.header-image img {
  max-width: 100%;
  height: auto;
  /* Ensure the image scales correctly */
}
</style>
