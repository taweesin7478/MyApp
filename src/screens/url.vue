<template>
  <view class="container">
    <text-input class="input" v-model="url" placeholder="URL" />

    <button title="join" color="rgb(27, 167, 46)" :onPress="chack" />
  </view>
</template>

<script>
import React, { useState } from "react";
import { Alert } from "react-native";
export default {
  data() {
    return {
      url: "",
      users: "",
      invite: [],
    };
  },
  props: {
    navigation: {
      type: Object,
    },
  },
  methods: {
    async manage(uuid) {
      const url = "https://meet.one.th/backend/api/rooms/check/" + uuid;
      var data = await fetch(url).then((res) => res.json());
      this.users = data;
      this.invite = [this.users.fullname, uuid];
      this.goToMeetScreen();
    },
    chack() {
      var uuid = this.url.split("=")[1];
      this.manage(uuid);
    },
    goToMeetScreen() {
      if (this.users["status"] == "Success") {
        this.navigation.navigate("Meet", {
          inviteBy: this.invite,
        });
      } else {
        Alert.alert(
          "Error",
          "Url ไม่ถูกต้อง",
          [{ text: "OK", onPress: () => console.log("OK Pressed") }],
          { cancelable: false }
        );
      }
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
