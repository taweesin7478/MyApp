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
      users: "",
      url: "",
    };
  },
  props: {
    navigation: {
      type: Object,
    },
  },
  created() {
    this.manage();
  },
  methods: {
    manage() {
      this.data = this.navigation.state.params.inviteBy;
      this.users = this.data[0];
      this.url = this.data[1];
    },
    onPressLearnMore: function () {
      Alert.alert("Success", "URL : " + this.url, [{ text: "OK" }], {
        cancelable: false,
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
</style>
