<template>
  <div>
    <WorldProfileUpdateDeck />
    <div style="height: 80px; font-size: 30px;"></div>
    <WorldCardDetail/>
		<div class="profile-box">
			<PublicProfile />
		</div>
    <button @click="updateAttackDeck">공격덱구성하기</button>
    <button @click="updateDefenseDeck">방어덱구성하기</button>
    <div class="profile-icon">
			<ProfileIconList />
		</div>
    <div class="profile-itemlist">
      <WorldProfileMyCardList />
    </div>
    <WorldProfileBattleLogList/>


  </div>
</template>

<script>
import ProfileIconList from '@/components/ProfileIconList'
import PublicProfile from "@/components/PublicProfile";
import WorldProfileBattleLogList from '@/components/world/profile/WorldProfileBattleLogList'
import WorldCardDetail from '@/components/world/profile/WorldCardDetail'
import WorldProfileMyCardList  from '@/components/world/profile/WorldProfileMyCardList'
import WorldProfileUpdateDeck  from '@/components/world/profile/WorldProfileUpdateDeck'

export default {
  name: 'WorldProfileView',
  components: {
    PublicProfile,
    ProfileIconList,
    WorldProfileBattleLogList,
    WorldCardDetail,
    WorldProfileMyCardList,
    WorldProfileUpdateDeck
  },
  computed: {
    user() {
      return this.$store.state.userObject
    },
		isLogin() {
			return this.$store.getters.isLogin;
		},    
  },
  methods: {
    updateAttackDeck() {
      const bodyScroll = document.querySelector("body");
			bodyScroll.style.overflow = "hidden";
      this.$store.commit('SHOW_DECKCARD_DETAIL', 'attack');
    },
    updateDefenseDeck() {
      const bodyScroll = document.querySelector("body");
			bodyScroll.style.overflow = "hidden";
      this.$store.commit('SHOW_DECKCARD_DETAIL', 'defense');
    }
  },
	created() { {
			if (!this.isLogin) {
				this.$router.push({ name: 'login'});
			}
		}
	},  
}
</script>

<style scoped>
.profile-worlddeck {
  border: 1px white solid;
	width: 70vw;
  margin: auto;
}
.profile-box {
	width: 80vw;
	height: 230px;
	margin: 0px auto;
	/* border: 1px solid whitesmoke; */
}
.profile-icon {
	width: 70vw;
	margin: 30px auto;
}
.profile-itemlist {
	width: 70vw;
	margin: auto;
}



</style>