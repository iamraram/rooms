<template>
  <div class="main">
    <div class="popup_art_board">

      <div class="value">
        <div class="value_child">
          <div class="value_title">
            추가할 오브젝트 정보
          </div>
          <div class="popup_art_board_width">
            오브젝트의 가로 크기를 입력하세요.
          </div>
          <div class="popup_art_board_box">
            <input type="number" class="popup_art_board_input white" min="1" max="500" v-model="width_new">
            <div class="popup_art_board_placeholder">cm</div>
          </div>
          <div class="popup_art_board_width">
            오브젝트의 세로 크기를 입력하세요.
          </div>
          <div class="popup_art_board_box">
            <input type="number" class="popup_art_board_input white" min="1" max="500" v-model="height_new">
            <div class="popup_art_board_placeholder">cm</div>
          </div>
          <div class="popup_art_board_width">
            오브젝트의 이름을 입력하세요.
          </div>
          <div class="popup_art_board_box">
            <input type="text" class="popup_art_board_input white names" maxlength="9" v-model="name_new">
          </div>
          <button type="button" class="popup_art_board_button" @click="add(width_new, height_new, name_new, total_object)">
            오브젝트 추가하기
          </button>
        </div>
      </div>

      <div class="popup_art_board_parent">
        <div class="popup_art_board_child">

            <div v-for="num_values in 50"
                 :key="num_values"
                 v-bind:id="naming(num_values)"
                 style="display: none">
            </div>

          <div class="visible">
            <div class="popup_art_board_title">
              방 크기를 정해주세요.
            </div>
            <div class="popup_art_board_width">
              방 가로 크기를 적어주세요. (최대 5M)
            </div>
            <div class="popup_art_board_box">
              <input type="number" class="popup_art_board_input" min="1" max="500" v-model="width_room">
              <div class="popup_art_board_placeholder">cm</div>
            </div>
            <div class="popup_art_board_width">
              방 세로 크기를 적어주세요. (최대 5M)
            </div>
            <div class="popup_art_board_box">
              <input type="number" class="popup_art_board_input" min="1" max="500" v-model="height_room">
              <div class="popup_art_board_placeholder">cm</div>
            </div>
            <div class="popup_art_board_box">
              <button type="button" class="popup_art_board_button" @click="start()">
                {{ Math.round( ((width_room / 100) * (height_room / 100)) / 3.3058 * 100) / 100 }}평 방 만들기
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      width_room: 0,
      height_room: 0,
      room_size: 0,
      width_new: 0,
      height_new: 0,
      name_new: '',
      total_object: 1
    }
  },
  methods: {
    start() {
      document.querySelector('.popup_art_board').style.backgroundColor = 'white';

      document.querySelector('.popup_art_board_child').style.backgroundColor = 'rgb(245, 245, 245)';
      document.querySelector('.popup_art_board_child').style.borderRadius = '0';
      document.querySelector('.popup_art_board_child').style.border = '1px solid rgb(0, 0, 0)';
      document.querySelector('.popup_art_board_child').style.justifyContent = 'center';
      document.querySelector('.popup_art_board_child').style.alignItems = 'center';

      document.querySelector('.visible').style.display = 'none';

      document.querySelector('.value').style.display = 'flex';
      document.querySelector('.popup_art_board').style.display = 'flex';
      document.querySelector('.popup_art_board').style.justifyContent = 'space-between';
      document.querySelector('.popup_art_board_parent').style.width = '80%';
      document.querySelector('.popup_art_board_parent').style.display = 'flex';
      document.querySelector('.popup_art_board_parent').style.justifyContent = 'center';
      document.querySelector('.popup_art_board_parent').style.alignItems = 'center';

      document.querySelector('.popup_art_board_child').style.width = this.width_room * 1.6 + 'px';
      document.querySelector('.popup_art_board_child').style.height = this.height_room * 1.6 + 'px';
    },

    add(width, height, name, total_object) {
      console.log('.object' + total_object)
      document.querySelector('#object' + total_object).style.display = 'flex';
      document.querySelector('#object' + total_object).style.backgroundColor = 'black';
      document.querySelector('#object' + total_object).style.color = 'white';
      document.querySelector('#object' + total_object).style.width = width * 1.6 + 'px';
      document.querySelector('#object' + total_object).style.height = height * 1.6 + 'px';
      document.querySelector('#object' + total_object).style.position = "absolute";
      document.querySelector('#object' + total_object).style.cursor = 'pointer';
      document.querySelector('#object' + total_object).style.fontSize = '13px';
      document.querySelector('#object' + total_object).style.justifyContent = 'center';
      document.querySelector('#object' + total_object).style.alignItems = 'center';
      document.querySelector('#object' + total_object).innerHTML = name;

      this.total_object += 1
    },
    naming(num) {
      return ('object' + num)
    },
  }
}
</script>

<style>

body {
  margin: 0;
  height: 100%;
}

div {
  box-sizing: border-box;
}

.value_title {
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 20px;
}

.value_child {
  display: flex;
  height: 400px;
  flex-direction: column;
  justify-content: space-between;
}

.value {
  display: none;
  padding: 30px;
  width: 20%;
  height: 100%;
  border: 1px solid black;
  background-color: rgb(245, 245, 245);
  flex-direction: column;
}

.popup_art_board {
  transition-duration: 1.5s;
  width: 100%;
  position: absolute;
  top: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.popup_art_board_child {
  transition-duration: 1.5s;
  width: 400px;
  height: 420px;
  border: 1px solid white;
  background-color: white;
  border-radius: 25px;
}

.visible {
  width: 400px;
  height: 420px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 40px;
}

.popup_art_board_title {
  font-weight: 600;
  font-size: 25px;
}

.popup_art_board_box {
  display: flex;
  flex-direction: row;
}

.white {
  background-color: rgb(245, 245, 245);
  margin-bottom: 20px;
}

.popup_art_board_input {
  transition-duration: 0.2s;
  width: 60px;
  border: none;
  border-bottom: 2px solid gray;
  margin-right: 10px;
  padding: 5px;
  font-size: 17px;
}

.popup_art_board_placeholder {
  position: relative;
  font-size: 17px;
  color: gray;
  top: 5px;
}

input:focus,
input:active {
  outline: none;
}

.popup_art_board_input:active,
.popup_art_board_input:focus {
  transition-duration: 0.2s;
  border-bottom: 2px solid orange;
}

.popup_art_board_button {
  transition-duration: 0.2s;
  width: 150px;
  height: 40px;
  border: 1px solid orange;
  border-radius: 15px;
  background-color: white;
  font-size: 15px;
}

.popup_art_board_button:hover {
  transition-duration: 0.2s;
  background-color: orange;
  color: white;
  font-weight: 600;
}

.names {
  width: 160px;
}

</style>
