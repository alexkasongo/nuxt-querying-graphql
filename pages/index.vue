<template>
  <div class="container">
    <div>
      <h1 class="text-4xl font-semi-bold text-gray-800">
        Nuxt.js Querying a GraphQL API
      </h1>
      <h2 class="text-2xl">
        {{ character.id }}. {{ character.name }}:
        {{ character.status }}
      </h2>
      <button
        class="inline-block px-6 py-2 text-xs font-medium leading-6 text-center text-white uppercase transition bg-blue-700 rounded shadow ripple hover:shadow-lg hover:bg-blue-800 focus:outline-none"
        @click="characterId = characterId + 1"
      >
        Next Character
      </button>
      <button
        class="inline-block px-6 py-2 text-xs font-medium leading-6 text-center text-white uppercase transition bg-blue-700 rounded shadow ripple hover:shadow-lg hover:bg-blue-800 focus:outline-none"
        @click="characterId = characterId - 1"
      >
        Prev Character
      </button>
      <ul v-for="character in characters.results" :key="character.id">
        <li>
          {{ character.name }}:
          {{ character.status }}
        </li>
      </ul>
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
    // Dynamic
    character: {
      query: gql`
        query getCharacter($id: ID!) {
          character(id: $id) {
            id
            name
            status
          }
        }
      `,
      variables() {
        return {
          id: this.characterId,
        }
      },
    },
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
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
