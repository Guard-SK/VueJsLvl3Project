<template>
  <div v-for="item in $store.getters.item_list_value" :key="item.id">
    <div class="item_container" v-if="item.deleted == false">
      <div class="top_container">
        <p>{{ item.message }}</p>
        <div class="actions">
          <img
            @click="$store.commit('editItem', item.id, item.message)"
            class="edit"
            src="../assets/edit.png"
          />
          <img
            @click="item.deleted = true"
            class="delete"
            src="../assets/deleted_icon.png"
          />
        </div>
      </div>
      <div
        class="edit_container"
        v-bind:class="{ 'display-flex': getEditClass(item.id) }"
      >
        <textarea
          id="edittextarea"
          class="edittextarea"
          rows="4"
          cols="50"
          v-model="item.message"
        ></textarea>
        <div class="edit_action_buttons">
          <button @click="discardBtn(item.id)" class="discardEditbtn">
            Discard Edit
          </button>
          <!-- TODO: Discard button -->
          <button
            class="submitEditbtn"
            @click="$store.commit('submitBtn', item.id)"
          >
            Submit Edit
          </button>
          <!-- TODO: Submit button -->
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'ToDoList',
    methods: {
      getEditClass(id) {
        console.log(this.$store.state.editObject[id.toString()])
        if (this.$store.state.editObject[id.toString()] == true) {
          return
        } else if (this.$store.state.editObject[id.toString()] == false) {
          return 'display-none'
        } else {
          return 'display-none'
        }
      },
      discardBtn(id) {
        this.$store.state.isEditingActive = false
        let txtarea = document.getElementById('edittextarea')
        txtarea.value = this.$store.state.editText
        this.$store.state.editText = ''
        this.$store.state.editObject[id.toString()] = false
      },
    },
  }
</script>
<style>
  .display-flex {
    display: flex !important;
  }
  .display-none {
    display: none;
  }
  .edit_action_buttons {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 0px;
    gap: 5px;

    flex: none;
    order: 1;
    flex-grow: 0;
  }
  .edit_container {
    display: none;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 0px;
    gap: 5px;

    flex: none;
    order: 1;
    flex-grow: 0;
  }
  .top_container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding: 0px;
    gap: 5px;

    width: 100%;

    flex: none;
    order: 0;
    flex-grow: 0;
  }
  .item_container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 16px 0px;
    gap: 5px;

    border-width: 1px 0px;
    border-style: solid;
    border-color: #000000;

    margin: 10px 0px;
  }
  .delete {
    width: 20px;
    height: 20px;
  }
  .edit {
    width: 20px;
    height: 20px;
  }
  .actions {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 0px;
    gap: 10px;

    flex: none;
    order: 1;
    flex-grow: 0;
  }
</style>
