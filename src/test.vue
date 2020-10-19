<template>
  <app-navigator></app-navigator>
</template>

<script>
import { createAppContainer, createStackNavigator } from "vue-native-router";

import UrlScreen from "./screens/url";
import MeetScreen from "./screens/meet";
import JoinScreen from "./screens/join";

const StackNavigator = createStackNavigator(
  {
    Url: UrlScreen,
    Meet: MeetScreen,
    Join: JoinScreen,
  },
  {
    initialRouteName: "Url",
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator },
};
</script>