<template>
  <!-- App -->
  <div id="app" ref="apphome">

    <!-- Statusbar -->
    <f7-statusbar></f7-statusbar>

    <!-- Left Panel -->
    <pleft></pleft>

    <!-- Right Panel -->
    <f7-panel right cover layout="dark">
      <f7-view id="right-panel-view" navbar-through :dynamic-navbar="true">
        <f7-navbar v-if="$theme.ios" title="Right Panel" sliding></f7-navbar>
        <f7-pages>
          <f7-page>
            <f7-navbar v-if="$theme.material" title="Right Panel" sliding></f7-navbar>
            <f7-block>
              <p>Right panel content goes here</p>
            </f7-block>
            <f7-block-title>Load page in panel</f7-block-title>
            <f7-list>
              <f7-list-item link="/about/" title="About"></f7-list-item>
              <f7-list-item link="/form/" title="Form"></f7-list-item>
            </f7-list>
            <f7-block-title>Load page in main view</f7-block-title>
            <f7-list>
              <f7-list-item link="/about/" title="About" link-view="#main-view"
                            link-close-panel></f7-list-item>
              <f7-list-item link="/form/" title="Form" link-view="#main-view"
                            link-close-panel></f7-list-item>
            </f7-list>
          </f7-page>
        </f7-pages>
      </f7-view>
    </f7-panel>

    <!-- Popup -->
    <lotterymethodpopup></lotterymethodpopup>
    <lotterychoosepopup></lotterychoosepopup>
    <lotteryautotrace></lotteryautotrace>
    <lotterytip></lotterytip>

    <!-- Popup Pankou -->
    <pkchoosepopup></pkchoosepopup>
    <pkchoosemethod></pkchoosemethod>

    <!-- Main Views -->
    <f7-views>
      <f7-view id="main-view" main domCache>
        <!-- Pages -->
        <f7-pages ref="tp">
          <homepage ref="hp"></homepage>
        </f7-pages>
        <chatRoom :newM="newMessageTip" ref="chatRoom" :class="showChatRoom?'chatRoomRoot':'chatRoomRootClose'" :alClick="changShowChatRoom"></chatRoom>
        <span class="messageChat" :class="{'newMessage':newMessage}" v-if="!showChatRoom" @click="showChatRoom=true;newMessage=false"><img src="/m/chatRoom_show.png" alt=""></span>
        <bottomtoolbar :alClick="changShowChatRoom"></bottomtoolbar>
        <newpersonhelp></newpersonhelp>
      </f7-view>
    </f7-views>
    <!-- Login Screen -->
  </div>
</template>

<script>
	import config from './config';
	import homepage from './pages/home.vue'
	import bottomtoolbar from './pages/bottom/nav.vue'
	import lotterymethodpopup from './pages/lottery/method.vue'
	import lotterychoosepopup from './pages/lottery/choose.vue'
	import pkchoosepopup from './pages/lottery/choosepk.vue'
	import pkchoosemethod from './pages/lottery/pkmethod.vue'
	import lotteryautotrace from './pages/lottery/trace.vue'
	import lotterytip from './pages/lottery/tip.vue'
	import lotteryzuo from './pages/lottery/zuo.vue'
	import pleft from './pages/left.vue'
	import loginscreen from './pages/login/loginscreen.vue'
	import newpersonhelp from './pages/home/newPersonHelp.vue'
	import chatRoom from './pages/chatRoom.vue'

	import store from './store'

	export default {
		components: {
			homepage,
			bottomtoolbar,
			loginscreen,
			lotterymethodpopup, pkchoosepopup, pkchoosemethod,
			lotteryautotrace,
			lotterytip,
			lotteryzuo,
			lotterychoosepopup,
			pleft,
			newpersonhelp,
			chatRoom,
		},
    data(){
			return {
				showChatRoom:false,
				newMessage:false,
      }
    },
		store: store,
		methods: {
			reloadhome: function () {
				this.$refs.hp.reloadmy();
			},
			reloadnotice: function () {
				this.$refs.hp.clicklogo();
			},
			reloadnum: function () {
				//console.log(this.$refs.tp);
				var topages = this.$refs.tp;
				if (topages.$children.length > 1) {
					//console.log(typeof topages.$children[1].testm);
					if (typeof topages.$children[1].testm != 'undefined') {
						topages.$children[1].testm();
					}
				}
				//this.$refs.tp.testm();
			},
			reloadsec: function () {
				var topages = this.$refs.tp;
				//console.log(topages.$children,'reloadsecreloadsec');
				if (topages.$children.length > 1) {
					var ltpage = topages.$children[1];
					if (ltpage.$el.id != 'lottery') {
						ltpage = topages.$children[2];
					}
					//console.log(ltpage.$el.id,'ltpage.$el.idltpage.$el.id');
					if (typeof ltpage.readMethod != 'undefined') {
						//console.log('readMethodreadMethod');
						ltpage.readMethod();
					}
				}
			},
			reloadlt: function (id) {
				//console.log(this.$refs.tp);
				var topages = this.$refs.tp;
				//console.log(topages,this.$refs);
				if (topages.$children.length > 1) {
					//console.log(typeof topages.$children[1].testlt,'testlttestlt');
					//console.log(topages.$children[1].$el.id);
					if (topages.$children[1].$el.id == 'buy' || topages.$children[1].$el.id == 'bonusopen' || topages.$children[1].$el.id == 'home') {
						if (typeof topages.$children[2].testlt != 'undefined') {
							topages.$children[2].testlt(id);
						}
					} else {
						if (typeof topages.$children[1].testlt != 'undefined') {
							topages.$children[1].testlt(id);
						}
					}

				}
				//this.$refs.tp.testm();
			},
			reloadpk: function (id) {

				var topages = this.$refs.tp;
				//console.log('reloadpkreloadpkreloadpk',topages.$children[1].$el.id,topages.$children[2].$el.id);
				if (topages.$children.length > 1) {
					if (topages.$children[1].$el.id == 'buy' || topages.$children[1].$el.id == 'bonusopen' || topages.$children[1].$el.id == 'home' || topages.$children[2].$el.id == 'pankoulhc') {
						if (typeof topages.$children[2].testlt != 'undefined') {
							topages.$children[2].testlt(id);
						}
					} else {
						if (topages.$children[2].$el.id != 'pankou') {
							if (typeof topages.$children[1].testlt != 'undefined') {
								topages.$children[1].testlt(id);
							}
						}
						if (topages.$children[2].$el.id == 'pankou') {
							if (typeof topages.$children[2].testlt != 'undefined') {
								topages.$children[2].testlt(id);
							}
						}
						if (topages.$children[1].$el.id != 'pankoulhc' && topages.$children[2].$el.id != 'pankou') {
							if (typeof topages.$children[1].testlt != 'undefined') {
								topages.$children[1].testlt(id);
							}
						}
					}

				}
				//this.$refs.tp.testm();
			},
			reloadpklhc: function (id) {

				var topages = this.$refs.tp;
				//console.log('reloadpklhcreloadpklhcreloadpklhcreloadpklhcreloadpklhc',topages.$children[1].$el.id,topages.$children[2].$el.id);
				// f7.views.main.activePage.name
				if (topages.$children.length > 1) {
					if (topages.$children[1].$el.id == 'buy' || topages.$children[1].$el.id == 'bonusopen' || topages.$children[1].$el.id == 'home') {
						if (typeof topages.$children[2].testlt != 'undefined' && topages.$children[2].$el.id != 'pankou') {
							topages.$children[2].testlt(id);
						}
					} else {
						if (topages.$children[2].$el.id != 'pankou') {
							if (typeof topages.$children[1].testlt != 'undefined') {
								topages.$children[1].testlt(id);
							}
						}
						if (topages.$children[1].$el.id != 'pankoulhc' && topages.$children[2].$el.id != 'pankou') {
							if (typeof topages.$children[2].testlt != 'undefined') {
								topages.$children[2].testlt(id);
							}
						}
					}

				}
				//this.$refs.tp.testm();
			},
			reloadsecpk: function (id, name) {
				var topages = this.$refs.tp;
				if (topages.$children.length > 1) {
					if (topages.$children[1].$el.id == 'buy' || topages.$children[1].$el.id == 'bonusopen' || topages.$children[1].$el.id == 'home' || topages.$children[1].$el.id == 'pankoulhc') {
						if (typeof topages.$children[2].secchg != 'undefined' && f7.views.main.activePage.name == 'pankou' && topages.$children[2].$el.id == 'pankou') {
							topages.$children[2].secchg(id, name);
						}
						if (typeof topages.$children[1].secchg != 'undefined' && f7.views.main.activePage.name == 'pankou' && topages.$children[1].$el.id == 'pankou') {
							topages.$children[1].secchg(id, name);
						}
						if (typeof topages.$children[2].secchg != 'undefined' && f7.views.main.activePage.name == 'pankoulhc' && topages.$children[2].$el.id == 'pankoulhc') {
							topages.$children[2].secchg(id, name);
						}
						if (typeof topages.$children[1].secchg != 'undefined' && f7.views.main.activePage.name == 'pankoulhc' && topages.$children[1].$el.id == 'pankoulhc') {
							topages.$children[1].secchg(id, name);
						}
					} else {
						if (typeof topages.$children[2].secchg != 'undefined' && f7.views.main.activePage.name == 'pankou' && topages.$children[2].$el.id == 'pankou') {
							topages.$children[2].secchg(id, name);
						}
						if (typeof topages.$children[1].secchg != 'undefined' && f7.views.main.activePage.name == 'pankou' && topages.$children[1].$el.id == 'pankou') {
							topages.$children[1].secchg(id, name);
						}
						if (typeof topages.$children[2].secchg != 'undefined' && f7.views.main.activePage.name == 'pankoulhc' && topages.$children[2].$el.id == 'pankoulhc') {
							topages.$children[2].secchg(id, name);
						}
						if (typeof topages.$children[1].secchg != 'undefined' && f7.views.main.activePage.name == 'pankoulhc' && topages.$children[1].$el.id == 'pankoulhc') {
							topages.$children[1].secchg(id, name);
						}
					}

				}
				//this.$refs.tp.testm();
			},
			remylist: function () {
				//console.log('remylistremylist');
				this.$refs.hp.reloadmy();
				this.$refs.hp.initswiper();
			},
			setopen: function () {
				this.$refs.lgsc.setopen();
			},
			getloginstate: function () {
				return this.$refs.lgsc.getinitopen();
			},
			cleanbasket: function () {
				var topages = this.$refs.tp;
				if (topages.$children.length > 1) {
					console.log(topages.$children[1].$el.id);
					if (topages.$children[1].$el.id == 'buy' || topages.$children[1].$el.id == 'bonusopen' || topages.$children[1].$el.id == 'home') {
						if (typeof topages.$children[2].testlt != 'undefined') {
							topages.$children[2].testlt(id);
						}
					} else {
						if (typeof topages.$children[1].testlt != 'undefined') {
							topages.$children[1].testlt(id);
						}
					}

				}
			},
      //关闭推送消息
			changShowChatRoom:function () {
				//如果在聊天室里面出来，就取消新消息震动效果
				this.showChatRoom&&(this.newMessage=false,this.$refs.chatRoom.closeNotice())
        //关闭聊天室
				this.showChatRoom=false
			},
      //新消息提示
      newMessageTip:function () {
        this.newMessage=true
      }
		},
		mounted: function () {
			/*if (config.chkmobile.Appcan() || config.chkmobile.iOS()) {
        $('#main-view').addClass('view-top');
      }*/
			//this.reloadhome();
		}
	}
</script>

<style lang="css">
  @import './assets/icon.css';
  @import './assets/reset.css';
  @import './assets/colors.css';
  @import './assets/app.css';

  .messageChat{
    color: #f60;
    cursor: pointer;
    width: 40px;
    height: 40px;
    position: fixed;
    right: -10px;
    top: 50%;
    z-index: 999999;
  }
  .messageChat img {
    width: inherit;
    height: inherit;
  }

  /*//动画效果  聊天室弹出*/
  @keyframes openChatRoom {
    from {left: 100%;}
    to {left: 0px;}
  }

  /*//动画效果  聊天室关闭*/
  @keyframes closeChatRoom {
    from {left: 0px;}
    to {left: 100%;}
  }
  /*//新消息提示，震动效果*/
  @keyframes newM {
    from {right: -10px;}
    to {right: 0px;}
  }


  .chatRoomRoot{
    animation: openChatRoom 0.5s;
    position: absolute;
    top: 0;
    left: 0;
  }
  .chatRoomRootClose{
    animation: closeChatRoom 0.5s;
    position: absolute;
    top: 0;
    left: 100%;
  }
  .newMessage{
    animation: newM 0.2s infinite linear alternate;
  }
</style>