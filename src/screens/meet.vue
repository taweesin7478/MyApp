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

    <button title="join" color="rgb(27, 167, 46)" :onPress="chack" />
  </view>
</template>

<script>
import { Alert } from "react-native";
export default {
  data() {
    return {
      name: "",
      users: "",
      data: [],
      invite: [],
      uuid: "",
    };
  },
  created() {
    this.manage();
  },
  props: {
    navigation: {
      type: Object,
    },
  },
  methods: {
    manage() {
      this.data = this.navigation.state.params.inviteBy;
      this.users = this.data[0];
      this.uuid = this.data[1];
    },
    chack() {
      if (this.name != "") {
        this.addName();
      } else {
        Alert.alert("Error", "กรุณาป้อนชื่อของคุณ", [{ text: "OK" }], {
          cancelable: false,
        });
      }
    },
    async addName() {
      const url = "https://meet.one.th/backend/api/rooms/unauth/joinroom";
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          roomuid: this.uuid,
          name: this.name,
          key: "",
        }),
      };
      const response = await fetch(url, requestOptions);
      const data = await response.json();
      this.invite = [this.users, data.url];
      this.goToJoinScreen();
    },
    goToJoinScreen() {
      this.navigation.navigate("Join", {
        inviteBy: this.invite,
      });
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
