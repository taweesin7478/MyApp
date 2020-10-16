<template>
  <view class="container">
    <!-- <view class="score">
      <text class="meeting">Meeting_Room</text>
    </view> -->
    <text-input class="input" v-model="name" placeholder="URL" />

    <button
      :on-press="onPressLearnMore"
      title="join"
      color="rgb(27, 167, 46)"
    />
  </view>
</template>

<script>
import { Alert } from "react-native";
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
  methods: {
    async data() {
      const url = "https://meet.one.th/backend/api/rooms/check/taw-ce5c-0a73";
      var data = await fetch(url).then((res) => res.json());
      this.users = data["fullname"];
    },
    onPressLearnMore: function () {
      Alert.alert(
        "Success",
        "สำเร็จแล้ว",
        [{ text: "OK", onPress: () => console.log("OK Pressed") }],
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
