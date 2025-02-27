<script setup lang="ts">
import { useCommunities } from "@/composables/useCommunities";
import { CommunityInterface } from "types";
const communities = useCommunities();
const search = ref("");
const filteredCommunities: Ref<CommunityInterface[]> = ref([]);

watchEffect(() => {
  const searchTerm = search.value.toLowerCase();

  if (searchTerm === "") {
    filteredCommunities.value = communities.value;
  } else {
    filteredCommunities.value = communities.value.filter((community) => {
      const communityName = community.name.toLowerCase();
      return communityName.includes(searchTerm);
    });
  }
});
</script>

<template>
  <div>
    <main>
      <div class="text-center mb-5 flex flex-col items-center gap-5">
        <h1 class="text-3xl sm:text-5xl md:text-7xl font-extrabold">
          Togo Tech <br />
          Communities
        </h1>
        <p class="text-gray-500">
          Discover the Thriving Tech Communities shaping Togo's Future.
        </p>

        <input
          type="search"
          name="search"
          id="search"
          v-model="search"
          placeholder="Search..."
          class="w-80"
        />
      </div>

      <div
        class="w-full z-50 rounded-lg p-3 grid grid-flow-row-dense sm:grid-cols-2 lg:grid-cols-3 gap-4"
      >
        <div
          class="p-3 flex flex-col gap-3 rounded-lg border-2 transition duration-500 ease-in-out hover:border-primary-500 dark:hover:border-primary-900 dark:border-gray-700"
          v-for="(community, index) in filteredCommunities"
          :key="index"
        >
          <div class="flex justify-center mb-4">
            <img
              :src="`/${community.image}`"
              class="rounded-full w-20"
              :alt="community.name + ' logo'"
            />
          </div>
          <h3 class="font-bold text-xl text-center">
            {{ community.name }}
          </h3>
          <p class="text-center text-sm">{{ community.description }}</p>
          <div class="flex flex-wrap gap-4 justify-center">
            <NuxtLink
              v-if="community.links.website"
              :to="community.links.website"
              target="_blank"
            >
              <i
                class="i-heroicons-globe-alt h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700 dark:hover:border-primary-900"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.github"
              :to="community.links.github"
              target="_blank"
            >
              <i
                class="i-bxl-github h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.telegram"
              :to="community.links.telegram"
              target="_blank"
            >
              <i
                class="i-bxl-telegram h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.twitter"
              :to="community.links.twitter"
              target="_blank"
            >
              <i
                class="i-bxl-twitter h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.discord"
              :to="community.links.discord"
              target="_blank"
            >
              <i
                class="i-bxl-discord-alt h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.linkedin"
              :to="community.links.linkedin"
              target="_blank"
            >
              <i
                class="i-bxl-linkedin h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.facebook"
              :to="community.links.facebook"
              target="_blank"
            >
              <i
                class="i-bxl-facebook-circle h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.instagram"
              :to="community.links.instagram"
              target="_blank"
            >
              <i
                class="i-bxl-instagram h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.whatsapp"
              :to="community.links.whatsapp"
              target="_blank"
            >
              <i
                class="i-bxl-whatsapp h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.meetup"
              :to="community.links.meetup"
              target="_blank"
            >
              <i
                class="i-mdi-meetup h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
            <NuxtLink
              v-if="community.links.youtube"
              :to="community.links.youtube"
              target="_blank"
            >
              <i
                class="i-mdi-youtube h-6 w-6 transition duration-100 ease-in-out hover:text-primary-700"
              />
            </NuxtLink>
          </div>
        </div>
      </div>

      <div v-if="filteredCommunities.length === 0">
        <p
          class="text-center text-xl sm:text-2xl md:tsext-3xl font-medium opacity-80"
        >
          Sorry, we did not find any results for" {{ search }} "
        </p>
      </div>

      <div
        class="fixed -z-50 right-16 -bottom-44 w-1/4 h-1/2 bg-gradient-to-r from-primary-400/20 to-cyan-400/20 blur-3xl rounded-full"
      ></div>
      <div
        class="dark:fixed -z-50 left-0 bottom-0 w-full h-full bg-gradient-to-r from-primary-400/10 to-cyan-400/10 blur-sm"
      ></div>
    </main>
  </div>
</template>
