<template>
  <div class="more" @click="isOpen = !isOpen">
    <p>...</p>
    <transition name="fade" appear>
      <div class="click-menu" v-if="isOpen">
        <button
          id="EditButton"
          @click.prevent="toggleModal({ active: true, id: id, type: 0 })"
        >
          Editar
        </button>
        <button id="deleteCollection" @click.prevent="rmvCollection">
          Excluir
        </button>
      </div>
    </transition>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  name: "dropDownCollection",
  data() {
    return {
      isOpen: false,
    };
  },
  props: ["id"],
  methods: {
    ...mapActions("collection", {
      deleteCollection: "deleteCollection",
    }),
    ...mapActions("modal", {
      toggleModal: "toggleModal",
    }),
    rmvCollection() {
      this.deleteCollection(this.id);
    },
  },
};
</script>

<style scoped>
.more {
  border-radius: 0 10px 10px 10px;
  padding: 10px;
  background: rgb(248, 248, 248);
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  cursor: pointer;
  position: absolute;
  z-index: 1;
  right: -15px;
}
.more p {
  display: true;
  margin-top: -10px;
}
#EditButton,
#deleteCollection {
  border: 1px solid black;
  border-radius: 5px;
}
#EditButton:hover,
#deleteCollection:hover {
  color: white;
  background-color: black;
  border-radius: 5px;
}
#EditButton {
  width: 54px;
  margin-bottom: 5px;
}


.click-menu {
  font-size: 13px;
}
.click-menu button {
  border: none;
  background-color: rgb(248, 248, 248);
  display: block;
}
</style>