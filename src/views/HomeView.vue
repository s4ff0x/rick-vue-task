<template>
  <div class="grid">
    <CharacterCard
      v-for="character in characters.results"
      :character="character"
      :key="character.id"
    ></CharacterCard>
  </div>
  <Pagination :characters="characters" :fetchPage="fetchPage"></Pagination>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import CharacterCard from "@/components/CharacterCard/CharacterCard.vue";
import axios from "axios";
import { API_BASE } from "@/utils/constants";
import { ICharacter, ICharacterResInfo } from "@/utils/types";
import Pagination from "@/components/Pagination/Pagination.vue"; // @ is an alias to /src

@Options({
  components: {
    Pagination,
    CharacterCard,
  },
  data() {
    return {
      characters: {}, //  TODO: how to pass types
    };
  },
  methods: {
    fetchPage(page: number) {
      // TODO: is it okay to pass function to pagination?
      axios
        .get<{ data: { results: ICharacter[]; info: ICharacterResInfo } }>( // TODO: is it okay ?
          `${API_BASE}/character/?page=${page}`
        )
        .then((r) => (this.characters = r.data));
    },
  },
  mounted: function () {
    axios
      .get<{ data: { results: ICharacter[]; info: ICharacterResInfo } }>( // TODO: is it okay ?
        `${API_BASE}/character`
      )
      .then((r) => (this.characters = r.data));
  },
})
export default class HomeView extends Vue {}
</script>

<style lang="scss">
.grid {
  width: 1024px;
  margin: 0 auto;
  display: grid;
  padding: 1rem;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 3rem;
  grid-template-rows: repeat(2, 1fr);
  padding-bottom: 100px;
}
</style>
