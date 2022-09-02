<!--TODO: extract shared ui components like title-->
<template>
  <div>
    <div class="flex-line">
      <div class="name">{{ character.name }}</div>
      <div class="status" :style="{ color: statusColor }">
        {{ character.status }}
      </div>
    </div>
    <div class="flex-line">
      <div class="gender">{{ character.gender }}</div>
      <div class="origin-name">{{ character.origin?.name }}</div>
    </div>
    <div class="image-container">
      <img :src="character.image" alt="Character" />
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { ICharacter } from "@/utils/types";

@Options({
  props: {
    character: Object, //  TODO: how to add type ICharacter ? Why duplication with class definition
  },
  computed: {
    statusColor() {
      // TODO: refactor this into map with values and place in utils
      if (this.character.status === "Dead") return "var(--red)";
      if (this.character.status === "Alive") return "var(--green)";
      return "--var(gray30)";
    },
  },
})
export default class CharacterCard extends Vue {
  character!: ICharacter; //  TODO: what is it?
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "./CharacterCard.scss";
</style>
