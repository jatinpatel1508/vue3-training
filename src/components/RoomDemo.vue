<template>
  <div class="room-wrapper">
    <div class="room-main" v-for="(room, index) in rooms" :key="index">
      <div class="room-title">Room - {{ index + 1 }}</div>
      <div class="persons">
        <div class="adult">
          <h4>Adult</h4>
          <button @click="addAdult(room)">+</button>
          <input class="adult-text" type="text" v-model="room.adult" disabled />
          <button @click="removeAdult(room)">-</button>
        </div>
        <div class="child">
          <h4>Child</h4>
          <button @click="addChild(room)">+</button>
          <input class="child-text" type="text" v-model="room.child" disabled />
          <button @click="removeChild(room)">-</button>
        </div>
      </div>
      <div class="add-remove-room">
        <button class="add-room" @click="addRoom()">Add Room</button>
        <button class="add-room" v-if="index != 0" @click="removeRoom(index)">
          Remove Room
        </button>
      </div>
    </div>
  </div>

  <button class="show-room-json" @click="isDisplayRoomJson = 1">
    Display Room JSON
  </button>
  <pre v-show="isDisplayRoomJson">{{ rooms }}</pre>
</template>

<script>
export default {
  name: "RoomDemo",
  components: {},
  props: {},
  data() {
    return {
      isDisplayRoomJson: 0,
      rooms: [
        {
          adult: 1,
          child: 0,
        },
      ],
    };
  },
  methods: {
    addRoom() {
      let tempRoom = {
        adult: 1,
        child: 0,
      };
      this.rooms.push(tempRoom);
    },
    removeRoom(index) {
      this.rooms.splice(index, 1);
    },
    addAdult(room) {
      room.adult += 1;
    },
    removeAdult(room) {
      room.adult -= room.adult != 1 ? 1 : 0;
    },
    addChild(room) {
      room.child += 1;
    },
    removeChild(room) {
      room.child -= room.child != 0 ? 1 : 0;
    },
  },
};
</script>

<style scoped>
/* ROOM DEMO CSS */
.room-wrapper {
  display: flex;
  border: 1px solid;
  padding: 15px;
  flex-wrap: wrap;
}
.room-main {
  width: 20%;
  border: 1px solid #ccc;
  padding: 10px;
  float: left;
  margin: 0 20px 10px 0px;
}
.persons {
  display: flex;
}
.adult {
  padding-right: 15px;
  width: 100px;
}
.adult > h4 {
  margin-bottom: 0px;
}
.adult-text {
  width: 30%;
  text-align: center;
}
.child {
  padding-right: 15px;
  width: 100px;
}
.child > h4 {
  margin-bottom: 0px;
}
.child-text {
  width: 30%;
  text-align: center;
}
</style>
