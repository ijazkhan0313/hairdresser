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

definePageMeta({
    middleware: ['auth']
})

// api calls 
const users = ref([]);
// Fetch data on component mount
onMounted(async () => {
  try {
    const response = await fetch('http://localhost:8000/api/get-clients');
    const data = await response.json();
    users.value = data.clients;
    console.log(data);
    
  } catch (error) {
    console.error('Error fetching users:', error);
  }
});

const deleteUser = async (id: number) => {
    try {
        await fetch(`http://localhost:8000/api/delete-user/${id}`, {
            method: 'POST',
        });
        users.value = users.value.filter((user) => user.id!== id);
    } catch (error) {
        console.error('Error deleting user:', error);
    }
}


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
                          All Clients
                        </BaseHeading>
                    </div>

                    <div class="mt-7 overflow-x-auto">
                        <div v-if="data === 0">
                            <BasePlaceholderPage title="Nothing to show"
                                subtitle="Looks like there are no transactions to show for this recipient. Come back one you have sent or received money from this recipient." />
                        </div>
                        <table v-else class="w-full whitespace-nowrap">
                            <thead>
                                <tr>
                                    <th class="py-2 text-left">#</th>
                                    <th class="py-2 text-left">Name</th>
                                    <th class="px-4 py-2 text-left">Email</th>
                                    <th class="px-4 py-2 text-left">Register at</th>
                                    <!-- <th class="px-4 py-2 text-left">Edit</th> -->
                                    <th class="px-4 py-2 text-left">Delete</th>
                                </tr>
                            </thead>

                            <tbody>
                                <tr v-for="(user, index) in users" :key="user.id" tabindex="0">
                                  <td class="py-2">
                                    <BaseText size="sm" weight="medium" lead="none" class="text-muted-400">
                                      {{ index + 1 }}
                                    </BaseText>
                                  </td>
                                  <td class="py-2">
                                    <BaseText size="sm" weight="medium" lead="none" class="text-muted-600 dark:text-muted-300">
                                      {{ user.name }}
                                    </BaseText>
                                  </td>
                                  <td class="px-4 py-2">
                                    <BaseText size="sm" weight="semibold" lead="none" class="text-muted-800 dark:text-muted-100">
                                      {{ user.email }}
                                    </BaseText>
                                  </td>
                                  <td class="px-4 py-2">
                                    <BaseText size="sm" weight="medium" lead="none" class="text-muted-600 dark:text-muted-300">
                                      {{ new Date(user.created_at).toLocaleDateString() }}
                                    </BaseText>
                                  </td>
                                  <!-- <td class="px-4 py-2">
                                    <NuxtLink :to="`/dashboards/edit-user/${user.id}`" class="text-blue-500 hover:underline">Edit</NuxtLink>
                                  </td> -->
                                  <td class="px-4 py-2">
                                    <button @click="deleteUser(user.id)" class="text-red-500 hover:underline">Delete</button>
                                  </td>
                                </tr>
                              </tbody> 
                        </table>
                    </div>
                </BaseCard>
            </div>
        </div>
    </div>
</template>
