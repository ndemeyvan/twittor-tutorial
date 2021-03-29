<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <!-- <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__admin-badge" v-else>Not Admin</div> -->
      <div class="user-profile__follower-count">
        <strong> Followers : </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__twoos-wrapper">
      <!-- <strong>{{item.content}} -- {{index}} </strong> -->
      <twoot-item
        v-for="item in user.twoots"
        :key="item.id"
        :username="user.username"
        :twoot="item"
        @favoriteTwoot="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";
export default {
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "Temistocle",
        firstname: "Yvan",
        lastname: "Ndeme",
        email: "ndemeyvan@gmail.com",
        isAdmin: false,
        twoots: [
          { id: 0, content: "Twooter is amazing" },
          { id: 1, content: "Twooter is not amazing" },
          { id: 2, content: "Everything is okay" },
          { id: 3, content: "I love seven Academy" },
        ],
      },
    };
  },
  components: {
    TwootItem,
  },

  methods: {
    addFollowers() {
      this.followers++;
    },

    toggleFavorite(id) {
      console.log(`This is the favorite twoot #${id}`);
    },
  },

  mounted() {
    console.log("Mounter called");
    this.addFollowers();
  },

  watch: {
    followers(newfollowersCound, olfFollowrCount) {
      if (olfFollowrCount < newfollowersCound) {
        console.log(` ${this.user.username} has gained a follower !!! `);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`;
    },
  },
};
</script>

<style >
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}
.user-profile__user-panel {
  display: grid;
  flex-direction: column;
  margin: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
/* .user-profile__admin-badge {
  background: purple;
  color: #fff;
  border-radius: 5px;
  margin-right: auto;
  padding: 0px 10px;
  font-weight: bold;
} */
</style>