<template>
  <div>
    <div class="home-title">Personal Boards</div>
    <div class="board-list" ref="boardList">
      <div
        class="board-item"
        v-for="b in boards"
        :key="b.id"
        :data-bgcolor="b.bgColor"
        ref="boardItem"
      >
        <router-link :to="`/b/${b.id}`">
          <div class="board-item-title">{{ b.title }}</div>
        </router-link>
      </div>
      <div class="board-item board-item-new">
        <a class="new-board-btn" href="" @click.prevent="addBoard">
          create new board...
        </a>
      </div>
    </div>
    <Modal></Modal>
  </div>
</template>

<script>
// import { mapState, mapGetters, mapMutations, mapActions } from 'vuex'
import { board } from "../api";
import Modal from "./Modal.vue";
// import AddBoard from './AddBoard.vue'

export default {
  // components: { AddBoard }, 
  components: { Modal }, 
    data() {
      return {
        loading: false,
        boards: [],
        error: "",
      };
    },
  computed: {
    // ...mapState({
    //   isAddBoard: 'isAddBoard',
    //   boardList: 'boardList'
    // }),
  },
  created() {
    this.fetchData();
    // this.FETCH_BOARD_LIST()
    // this.SET_THEME()
  },
  updated() {
    console.log(this.$refs.boardItem)
    this.$refs.boardItem.forEach((el) => {
      el.style.backgroundColor = el.dataset.bgcolor;
    });
    // Array.from(document.querySelectorAll('.board-item')).forEach(el => {
    //   el.style.backgroundColor = el.dataset.bgcolor || '#ddd'
    // })
  },
  // updated() {
    // this.$refs.boardItem.forEach(el => {
    //   el.style.backgroundColor = el.dataset.bgcolor
    // })
  // },
  methods: {
    fetchData() {
      this.loading = true;
      board
        .fetch()
        .then((data) => {
          console.info(data, data.list);
          this.boards = data.list;
        })
        .finally((_) => {
          this.loading = false;
        });
    },
    // ...mapMutations([
    //   'SET_IS_ADD_BOARD',
    //   'SET_THEME'
    // ]),
    // ...mapActions([
    //   'FETCH_BOARD_LIST',
    // ]),
    // onClickCreateBoard() {
    //   this.SET_IS_ADD_BOARD(true)
    // }
  },
};
</script>

<style>
.home-title {
  padding: 10px;
  font-size: 18px;
  font-weight: bold;
}
.board-list {
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
}
.board-item {
  width: 23%;
  height: 100px;
  margin: 0 2% 20px 0;
  border-radius: 3px;
}
.board-item a {
  text-decoration: none;
  display: block;
  width: 100%;
  height: 100%;
}
.board-item a:hover,
.board-item a:focus {
  background-color: rgba(0, 0, 0, 0.1);
  color: #666;
}
.board-item-title {
  color: #fff;
  font-size: 18px;
  font-weight: 700;
  padding: 10px;
}
.board-item a.new-board-btn {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
  height: 100px;
  width: inherit;
  color: #888;
  font-weight: 700;
}
</style>
