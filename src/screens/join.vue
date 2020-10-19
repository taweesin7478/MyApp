<template>
  <view class="container">
    <view>
      <text class="meeting">Meeting_Room</text>
    </view>
    <text class="invite">Invite by : {{ users }}</text>
    <button
      :on-press="onPressLearnMore"
      title="join"
      color="rgb(27, 167, 46)"
      accessibility-label="Learn more about this purple button"
    />
  </view>
</template>

<script>
import { Alert } from "react-native";
export default {
  data() {
    return {
      users: "98",
    };
  },
  created() {
    this.data();
  },
  methods: {
    async data() {
      const url = "https://meet.one.th/backend/api/rooms/check/taw-ce5c-0a73";
      var data = await fetch(url).then((res) => res.json());
      this.users = data["fullname"];
    },
    onPressLearnMore: function () {
      // Success
      Alert.alert(
        "Success",
        "สำเร็จแล้ว",
        [
          // {
          //   text: "Ask me later",
          //   onPress: () => console.log("Ask me later pressed"),
          // },
          // {
          //   text: "Cancel",
          //   onPress: () => console.log("Cancel Pressed"),
          //   style: "cancel",
          // },
          { text: "OK", onPress: () => console.log("OK Pressed") },
        ],
        { cancelable: false }
      );
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
</style>
