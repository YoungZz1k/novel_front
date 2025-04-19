<template>
  <div class="friend_link">

  </div>
</template>

<script>
import { reactive, toRefs, onMounted } from "vue";
import { listHomeFriendLinks } from "@/api/home";
export default {
  name: "FriendLink",
  setup() {
    const state = reactive({
      friendLinks: [],
    });

    onMounted(async () => {
      const { data } = await listHomeFriendLinks();
      state.friendLinks = data;
    });

    return {
      ...toRefs(state),
    };
  },
};
</script>
