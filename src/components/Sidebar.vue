<template>
  <v-navigation-drawer v-model="show" temporary app>
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title class="title">Enspire</v-list-item-title>
        <v-list-item-subtitle>Make CAS great again</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>
    <v-divider />
    <v-list nav dense>
      <v-list-item-group
        v-model="group"
        active-class="primary--text text--accent-4"
      >
        <v-list-item to="/">
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>首页</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider />
        <v-subheader>CAS管理</v-subheader>
        <v-list-item
          v-for="item in drawerItems"
          :key="item.title"
          :to="item.to"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider />
        <v-subheader>信息</v-subheader>
        <v-list-item to="/about">
          <v-list-item-icon>
            <v-icon>mdi-information</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>关于我们</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-navigation-drawer>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  watch: {
    group(): void {
      this.$emit("hide-sidebar");
    },
  },
  props: {
    drawer: Boolean,
  },
})
export default class Sidebar extends Vue {
  group = null;
  drawerItems = [
    { title: "我们的社团", icon: "mdi-view-dashboard", to: "/clubs" },
    { title: "预约教室", icon: "mdi-calendar", to: "/reservation" },
    {
      title: "申请请假",
      icon: "mdi-checkbox-marked-outline",
      to: "/askforleave",
    },
  ];
  get show(): boolean {
    return this.$props.drawer;
  }
  set show(newValue: boolean) {
    if (newValue === false) this.$emit("hide-sidebar");
  }
}
</script>
