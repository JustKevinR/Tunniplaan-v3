<template>
  <h1>Tunniplaan</h1>
  <select name="" id="" v-model="active" @change="getTimetable">
    <option value="0" selected>Vali rühm</option>
    <option v-for="group in groups" :key="group.groupId" :value="group.groupId">
      {{ group.groupCode }}
    </option>
  </select>
</template>

 

<script>
import { onMounted, ref } from "vue";
export default {
  setup() {
    const groups = ref([]);
    const active = ref(0);
    const timeTable = ref([]);

 

    const getGroups = async () => {
      groups.value = await (
        await fetch("https://be.ta19heinsoo.itmajakas.ee/api/groups")
      ).json();
    };

 

    const getTimetable = async () => {
      timeTable.value = await (
        await fetch(
          `https://be.ta19heinsoo.itmajakas.ee/api/lessons/groups=${active.value}&weeks=10`
        )
      ).json();
    };

 

    onMounted(getGroups);
    return {
      groups,
      active,
      getTimetable,
      timeTable,
    };
  },
};
</script>

 

<style>
</style>
 