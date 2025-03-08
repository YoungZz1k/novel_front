 <template>
  <div class="topMain">
    <div class="box_center cf">
      <router-link :to="{ name: 'home' }" class="logo fl"
        >
        <span class="logo-text">风云小说</span>
      </router-link>
      <div class="searchBar fl">
        <div class="search cf">
          <input
            v-model="keyword"
            type="text"
            placeholder="书名、作者、关键字"
            class="s_int"
            v-on:keyup.enter="searchByK"
          />
          <label class="search_btn" id="btnSearch" @click="searchByK()"
            ><i class="icon"></i
          ></label>
        </div>
      </div>

      <div class="bookShelf fr" id="headerUserInfo">
        <!--
        <a class="sj_link" href="/user/favorites.html">我的书架</a>-->
        <span v-if="!token" class="user_link"
          ><!--<i class="line mr20">|</i
          >-->
          <router-link :to="{ name: 'login' }" class="mr15">登录</router-link>
          <router-link :to="{ name: 'register' }" class="mr15"
            >注册</router-link
          >
        </span>
        <span v-if="token" class="user_link"
          ><!--<i class="line mr20">|</i
          >--><router-link :to="{name:'userSetup'}" class="mr15">{{ nickName }}</router-link>
          <a @click="logout" href="javascript:void(0)">退出</a></span
        >
      </div>
    </div>
  </div>
</template>

<script>
import logo from "@/assets/images/logo.png";
import { reactive, toRefs, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";
import { getToken, getNickName, removeToken, removeNickName,removeUid } from "@/utils/auth";
export default {
  name: "Top",
  setup(props, context) {
    const state = reactive({
      keyword: "",
      nickName: getNickName(),
      token: getToken(),
    });
    state.nickName = getNickName();
    state.token = getToken();
    const route = useRoute();
    const router = useRouter();
    state.keyword = route.query.key;
    const searchByK = () => {
      router.push({ path: "/bookclass", query: { key: state.keyword } });
      context.emit("eventSerch", state.keyword);
    };
    const logout = () => {
      removeToken();
      removeNickName();
      removeUid()
      state.nickName = "";
      state.token = "";
    };
    return {
      ...toRefs(state),
      logo,
      searchByK,
      logout,
    };
  },
};
</script>

 <style scoped>
 .logo-text {
   font-size: 32px;  /* 添加字号定义 */
   font-weight: 700;
   color: #fff;
   margin-left: 50px;
   position: relative;
   animation: neonGlow 1.5s ease-in-out infinite alternate; /* 添加动画声明 */
   text-shadow:
       0 0 5px #ff8800,  /* 修改颜色值 */
       0 0 10px #ff8800,
       0 0 20px #ff8800;
 }

 @keyframes neonGlow {
   from {
     text-shadow:
         0 0 2px #ff8800,  /* 修改颜色值 */
         0 0 4px #ff8800,
         0 0 6px #ff8800;
   }
   to {
     text-shadow:
         0 0 5px #ff8800,  /* 修改颜色值 */
         0 0 15px #ff8800,
         0 0 25px #ff8800;
   }
 }

 </style>
