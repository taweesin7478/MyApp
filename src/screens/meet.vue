<template>
  <view class="container">
    <view class="score">
      <text class="meeting">Meeting_Room</text>
    </view>
    <text class="invite">Invite by : {{ users }}</text>
    <text class="invite"
      >Please enter your name for display in the meeting.</text
    >
    <text-input class="input" v-model="name" placeholder="Enter your name" />

    <button title="join" color="rgb(27, 167, 46)" @press="goToJoinScreen" />
  </view>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      users: "",
    };
  },
  created() {
    this.data();
  },
  props: {
    navigation: {
      type: Object,
    },
  },
  methods: {
    async data() {
      const url = "https://meet.one.th/backend/api/rooms/check/taw-ce5c-0a73";
      var data = await fetch(url).then((res) => res.json());
      this.users = data["fullname"];
    },
    goToJoinScreen() {
      this.navigation.navigate("Join");
    },
  },
};
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
.meeting {
  margin-bottom: 10;
  font-size: 25;
}
.invite {
  margin-bottom: 15;
  font-size: 15;
}
.input {
  width: 200;
  height: 40;
  font-size: 15;
  border-width: 1;
  border-color: gray;
  margin-bottom: 15;
  padding: 10;
}
</style>
