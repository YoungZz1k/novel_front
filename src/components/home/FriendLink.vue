<template>
  <div class="friend_link">

  </div>
</template>

<script>
import { reactive, toRefs } from "vue";
export default {
  name: "FriendLink",
  setup() {
    const state = reactive({
      friendLinks: [],
    });

    // onMounted(async () => {
    //   try {
    //     const res = await listHomeFriendLinks();
    //     // 确保响应包含data字段
    //     if(res && res.data) {
    //       state.friendLinks = res.data;
    //     }
    //   } catch (error) {
    //     console.error("获取友链失败:", error);
    //   }
    // });

    return {
      ...toRefs(state),
    };
  },
};
</script>
