<template>
  <div class="container">
    <div>
      <h1 class="text-4xl font-semi-bold text-gray-800">
        Nuxt.js Querying a GraphQL API
      </h1>
      <div class="flex" v-if="!$apollo.queries.characters.loading">
        <ul class="w-64 px-2 text-gray-600">
          <li v-for="character in characters.results" :key="character.id">
            <nuxt-link
              :to="character.id"
              class="hover: text-bold hover:text-gray-900 leading-loose"
            >
              {{ character.name }}:
            </nuxt-link>
          </li>
        </ul>
        <div class="flex-grow bg-gray-900 min-h-full">
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
