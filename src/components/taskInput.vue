<template>
    <div class="inputBox shadow">

        <input type="text" v-model="taskItem" placeholder="Type what u have to do" v-on:keyup.enter="addTask" maxlength="20">
        <span class="addContainer" v-on:click="addTask">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>

        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고</h3>
            <span slot="body"></span>
            <span slot="footer" @click="showModal = false">
                할 일을 입력하세요.
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>

<script>
    import Modal from "./common/Modal";

    export default {
        components: {
            Modal: Modal
        },
        data() {
            return {
                taskItem: '',
                showModal: false
            }
        },
        methods: {
            addTask() {
            if(this.taskItem !== "") {
                let value = this.taskItem && this.taskItem.trim();
                this.$emit('addTask', value);
                this.clearInput();
            }else {
                this.showModal = !this.showModal;
            }
            },
            clearInput() {
              this.taskItem = '';
            }
        }

    }
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;

  }
  .inputBox input {
    /*border-style: none;*/
    font-size: 0.9rem;
    width: 80%;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>
