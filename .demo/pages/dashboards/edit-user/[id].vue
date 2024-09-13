<script setup lang="ts">
definePageMeta({
  title: 'Activity',
  preview: {
    title: 'Personal dashboard v1',
    description: 'For personal usage and reports',
    categories: ['dashboards'],
    src: '/img/screens/dashboards-personal-1.png',
    srcDark: '/img/screens/dashboards-personal-1-dark.png',
    order: 1,
  },
})


// my code 
import { useAuthStore } from '~/stores/auth'
const authStore = useAuthStore()



definePageMeta({
  middleware: ['auth']
})


// submnit handleSubmit

import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

// Define a ref to hold user data
const user = ref(null);
const name = ref('')
const email = ref('')

// Fetch user data when the component mounts
onMounted(async () => {
  try {
    const id = route.params.id;
    const response = await fetch(`http://localhost:8000/api/get-user/${id}`);
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    user.value = data.user; // Ensure data.user is valid
    console.log('User data fetched:', user.value.name);  // Log fetched data for debugging
  } catch (error) {
    console.error('Error fetching user data:', error);
  }
});

// Method to handle user update
const updateUser = async () => {
    const payload = {
    name: name.value,
    email: email.value,
  }

  try {
    const id = route.params.id;
    const response = await fetch(`http://localhost:8000/api/v1/update-user/${id}`, {
      method: 'post',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(payload),
    });
    if (!response.ok) {
      throw new Error('Failed to update user');
    }
    router.push('/dashboards/hairdresser'); // Navigate to a different page after updating
  } catch (error) {
    console.error('Error updating user:', error);
  }
};
</script>

<template>
  <div>
    <!-- Grid -->
    <div class="grid grid-cols-12 gap-6">
      <!--Transactions-->
      <div class="col-span-12">
        <BaseCard rounded="md" shadow="hover" class="p-8">
          <div class="mb-8 flex items-center justify-between">
            <BaseHeading as="h4" size="sm" weight="medium" lead="none" class="text-muted-400 uppercase">
              Update Hairdresser
             </BaseHeading>
             
             <BaseButton color="default" class="w-full sm:w-auto">
               <NuxtLink  to="/dashboards/hairdresser">Back</NuxtLink>
             </BaseButton>
          </div>
          <!-- form -->
          <form @submit.prevent="updateUser">
            <BaseInput
             v-model="name" name="name"
              rounded="md"
              label="User Name"
              placeholder="Ex: username"
            />
            <BaseInput
             v-model="email" name="email"
              rounded="md"
              label="Email"
              placeholder="email@gmail.com"
            />
            <button
              type="submit"
              class="nui-button nui-button-lg nui-button-rounded-sm nui-button-solid nui-button-primary w-full mt-3"
            >
              <span>Submit</span>
            </button>
          </form>
        </BaseCard>
      </div>
    </div>
  </div>
</template>
