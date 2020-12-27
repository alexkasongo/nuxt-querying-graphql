<template>
  <div class="container">
    <div class="rounded border m-2">
      <h1 class="p-2 text-4xl font-semi-bold text-gray-800">
        Nuxt.js Querying a GraphQL API
      </h1>
      <div class="flex p-2" v-if="!$apollo.queries.characters.loading">
        <ul class="w-100 px-2 rounded border text-gray-600">
          <li
            v-for="character in characters.results"
            :key="character.id"
            class="py-2"
          >
            <nuxt-link
              :to="character.id"
              class="w-full inline-block px-6 py-2 text-xs font-medium leading-6 text-center text-black uppercase transition bg-gray-100 rounded shadow ripple hover:shadow-lg hover:bg-gray-200 focus:outline-none"
            >
              {{ character.name }}:
            </nuxt-link>
          </li>
        </ul>
        <div class="flex-grow min-h-full">
          <nuxt-child :key="$route.params.id"></nuxt-child>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  data: () => ({
    characterId: 9,
  }),
  apollo: {
    characters: gql`
      query getCharacters {
        characters {
          results {
            id
            name
            status
          }
        }
      }
    `,
  },
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
}
</style>
