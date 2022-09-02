<!--TODO: how to make it properly ?-->
<template>
  <div class="wrapper">
    <div :class="{ selected: current === 1 }" @click="fetchPage(1)">1</div>

    <div v-if="current > 2">...</div>
    <div v-if="current > 2" @click="fetchPage(current - 1)">
      {{ current - 1 }}
    </div>
    <div
      v-if="current > 1 && current < pages"
      :class="{ selected: current > 1 }"
      @click="fetchPage(current)"
    >
      {{ current }}
    </div>
    <div v-if="current < pages - 1" @click="fetchPage(current + 1)">
      {{ current + 1 }}
    </div>
    <div v-if="current < pages - 1">...</div>

    <div :class="{ selected: current === pages }" @click="fetchPage(pages)">
      {{ pages }}
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { ICharacter } from "@/utils/types";

@Options({
  props: ["characters", "fetchPage"], //  TODO: analogically with CharacterCard
  computed: {
    current() {
      if (!this.characters.info?.next) return this.pages;
      const arr = this.characters.info?.next.split("=") || [1]; //  TODO: wtf?
      return +arr[arr.length - 1] - 1;
    },
    pages() {
      return +this.characters.info?.pages;
    },
  },
})
export default class Pagination extends Vue {
  characters!: ICharacter[]; //  TODO: analogically with CharacterCard
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "./Pagination.scss";
</style>
