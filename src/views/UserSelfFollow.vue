<template>
  <div class="rwd-container">
    <div class="follow-container">
      <div class="navbar">
        <Navbar />
      </div>
      <div class="middle-container scrollbar">
        <div class="follow-tabs">
          <UserFollowTabs :currentUser="currentUser" />
        </div>
        <router-view
          @tap-follow-button="tapFollowButton"
          :relateToUser="relateToUser"
        ></router-view>
      </div>
      <div class="related-users">
        <RelatedUsers
          :isFollowStatus="isFollowStatus"
          @related-to-userFollow="relatedToUserFollow"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "./../components/Navbar.vue";
import RelatedUsers from "./../components/RelatedUsers.vue";
import UserFollowTabs from "./../components/UserFollowTabs.vue";
import { mapState } from "vuex";

export default {
  name: "UserSelfFollow",
  components: {
    Navbar,
    UserFollowTabs,
    RelatedUsers,
  },
  data() {
    return {
      isFollowStatus: {},
      relatedFollowStatus: {},
      relateToUser: {},
    };
  },
  watch: {
    relatedFollowStatus(newValue) {
      this.relatedFollowStatus = newValue;
    },
  },
  methods: {
    tapFollowButton(payload) {
      this.isFollowStatus = payload;
    },
    relatedToUserFollow(payload) {
      this.relateToUser = payload;
    },
  },
  computed: {
    ...mapState(["currentUser"]),
  },
};
</script>

<style lang="scss" scoped>
@import "./src/assets/scss/main.scss";

.follow-container {
  display: grid;
  grid-template-columns: 0.9fr 600px 1fr;
  grid-gap: 30px;

  .navbar {
    grid-column: 1 / 2;
  }
  .middle-container {
    grid-column: 2 / 3;
  }
  .related-users {
    grid-column: 3 / 4;
  }
}

.middle-container {
  height: calc(100vh);
  overflow-y: scroll;
}

.scrollbar {
  padding-left: 1px;
  &::-webkit-scrollbar {
    width: 1px;
  }
  &::-webkit-scrollbar-thumb {
    border-radius: 3px;
    background-color: rgba(225, 222, 222, 0.1);
  }
}

@media screen and (max-width: 1359px) {
  .follow-container {
    grid-template-columns: 1fr 2fr 0.2fr;
    grid-gap: 10px;
    .navbar {
      grid-column: 1 / 2;
    }
    .middle-container {
      grid-column: 2 / 3;
    }
    .related-users {
      display: none;
    }
  }
}
</style>