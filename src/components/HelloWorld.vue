<template>
  <div class="page-test">

    <div>head</div>

    <div class="cube-page">
      <!--<div v-show="loading">-->
      <!--<cube-loading class="my-loading"></cube-loading>-->
      <!--</div>-->
      <div class="wrapper">
        <div class="content">
          <div class="content-scroll-wrapper">
            <div class="content-scroll-list-wrap" ref="scrollWrapper">
              <cube-scroll
                ref="contentScroll"
                :data="dataList"
                :options="options"
                @pulling-down="onPullingDown"
                @pulling-up="onPullingUp">
                <ul class="imgs-wrapper">
                  <li v-for="(item, index) in dataList" :key="index" class="imgs-item">
                    <div class="li-content" @load="onDataLoad">
                      <router-link :to="{name: 'HelloWorld'}" class="content-left">
                        <!-- <img src="../../assets/imgs/car.png"> -->
                        <div :class="{'pass' : (item.status == '4'), 'unpass': item.status == '5'}">
                          {{item.hphm}}
                        </div>
                      </router-link>
                      <div class="content-right"
                           @touchstart="gotouchstart(item)"
                           @touchend="gotouchend(item)"
                           @touchmove="gotouchmove">
                      <!--<div class="content-right"-->
                           <!--@click="showPop(item)">-->
                        <div><label>违法时间：</label>{{item.wfsj}}</div>
                        <div><label>违法地点：</label>{{item.wfdd}}</div>
                        <div><label>申请时间：</label>{{item.createDate}}</div>

                      </div>
                    </div>
                  </li>
                </ul>

                <cube-popup type="dialog" ref="popup" :zIndex="99"
                            :maskClosable="true"
                            position="center" @mask-click.stop="popHide">
                  <div class="pop">
                    <ul>
                      <li><router-link :to="{name: 'HelloWorld'}">编辑</router-link></li>
                      <li @click="deleteApply(selectedId)">删除</li>
                    </ul>
                  </div>
                </cube-popup>


                <template slot="pulldown" slot-scope="props">
                  <div v-if="props.pullDownRefresh"
                       class="cube-pulldown-wrapper"
                       :style="props.pullDownStyle">
                    <div v-if="props.beforePullDown"
                         class="before-trigger"
                         :style="{paddingTop: props.bubbleY + 'px'}">
                      <span :class="{rotate: props.bubbleY > 0}">↓</span>
                    </div>
                    <div class="after-trigger" v-else>
                      <div v-show="props.isPullingDown" class="loading">
                        <cube-loading></cube-loading>
                      </div>
                      <transition name="success">
                        <div v-show="!props.isPullingDown" class="text-wrapper"><span class="refresh-text">{{loadedText}}</span></div>
                      </transition>
                    </div>
                  </div>
                </template>
              </cube-scroll>
            </div>

            <div class="no-data" v-if="!loading && dataList.length == 0">暂无数据</div>
          </div>

        </div>
      </div>
    </div>
  </div>

</template>

<script>
/* eslint-disable */
  const dataList = [{
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }, {
    id: '1',
    status: '1',
    hphm: '13246',
    hpzl: '01',
    wfsj: '2019-05-21',
    createDate: '2019-05-22',
    wfdd: 'dsgfhgfgjhgjfghjkhkhg撒即可了解的了解过疯狂夺金'
  }]
  export default {
    name: 'HelloWorld',
    data () {
      return {
        activeIndex: 0,
        activeClass: '',
        loading: true,
        dataList: [],
        timeOutEvent: 0,
        loadedText: '',
        options: {
          pullDownRefresh: {
            threshold: 60,
            stopTime: 1000,
            txt: '更新成功'
          },
          pullUpLoad: true
        },
        secondStop: 26,
        selectedId: null
      }
    },
    created () {
      let page = sessionStorage.getItem('currPage')
      let status = sessionStorage.getItem('currStatus')
      if (page) {
        if (status) {
          this.params.status = status
          this.activeIndex = parseInt(status)
        }
        this.params.page = page
      } else {
        this.fetchData()
      }
    },
    methods: {
      fetchData () {
        this.dataList = this.dataList.concat(dataList)
      },
      gotouchstart (item) {
        let that = this
        this.timeOutEvent = setTimeout(function () {
          // 执行长按要执行的内容
          that.timeOutEvent = 0
          if (item.status === '1') {
            that.showPop(item)
          }
        }, 1500) // 这里设置定时
      },
      // 手释放，如果在500毫秒内就释放，则取消长按事件，此时可以执行onclick应该执行的事件
      gotouchend (item) {
        console.log('end')
        clearTimeout(this.timeOutEvent)
        if (this.timeOutEvent !== 0) {
          if (item.status === '1') {
            this.showPop(item)
          }
        }
      },
      // 如果手指有移动，则取消所有事件，此时说明用户只是要移动而不是长按
      gotouchmove () {
        clearTimeout(this.timeOutEvent) // 清除定时器
        this.timeOutEvent = 0
      },
      deleteDialog (id) {
        this.$createDialog({
          type: 'confirm',
          icon: 'cubeic-alert',
          title: '确认删除？',
          confirmBtn: {
            text: '确认',
            active: true,
            disabled: false,
            href: 'javascript:;'
          },
          cancelBtn: {
            text: '取消',
            active: false,
            disabled: false,
            href: 'javascript:;'
          },
          onConfirm: () => {
            this.deleteApply(id)
          },
          onCancel: () => {
          }
        }).show()
      },
      deleteApply (id) {
        this.dataList = _.remove(this.dataList, (item, index) => {
          return item.id !== id
        })
      },
      statusChange (index, value) {
        this.activeIndex = index
        this.params.status = value
        // this.$refs.contentScroll.scrollTop = 0
      },
      goback () {
        this.$router.push({name: 'Home'})
      },
      onPullingDown () {
        setTimeout(() => {
          this.dataList = []
          this.fetchData()
          this.$refs.contentScroll.scrollTo(0, this.secondStop, 300)
        }, 1000)
      },
      onPullingUp () {
        setTimeout(() => {
          // debugger
          this.fetchData()
        }, 1000)
      },
      onDataLoad () {
        const contentScroll = this.$refs.contentScroll
        contentScroll.scroll.beforePullDown && contentScroll.refresh()
      },
      showPop (item) {
        this.selectedId = item.id
        if (item.status === '1') {
          this.$refs.contentScroll.disable()
          this.showHello(item)
          // this.$refs.popup.show()
        }
      },
      popHide (e) {
        e.stopPropagation()
        this.enableClick = true
        this.$refs.contentScroll.enable()
      },
      showOperateDiag (item) {
        if (item.status !== '1') {
          return false
        }
        this.$createDialog({
          type: 'confirm',
          icon: 'cubeic-alert',
          title: '操作提示',
          content: '请选择操作',
          maskClosable: true,
          confirmBtn: {
            text: '编辑',
            active: true,
            disabled: false,
            href: 'javascript:;'
          },
          cancelBtn: {
            text: '删除',
            active: false,
            disabled: false,
            href: 'javascript:;'
          },
          onConfirm: () => {
            this.$router.push({name: 'recheck-apply-modify', params: {id: item.id}})
          },
          onCancel: (e) => {
            // 如果点击的是按钮
            if (e.target.tagName.toUpperCase() === 'A') {
              this.deleteDialog(item.id)
            }
          },
        }).show()
      },
      showHello(item) {
        // 直接调用
        // 传入配置对象，默认传入的所有对象全都当做 props 传入组件
        // 除了在调用 createAPI 的时候传入了 events，这里对应的就是
        // on{event name} 会被当做事件回调处理
        const instance = this.$createHello({
          content: 'My Hello Content',
          refName: 'mypop',
          itemId: item.id,
        })
        instance.$refs.mypop.show()
        this.$refs.contentScroll.enable()
      }
    },
    watch: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .page-test
    .loading {
      text-align: -webkit-center;
    }
    .status-radio {
      z-index 90;
      position: fixed;
      top: 12rem;
      width: 5rem;
      background-color: #c0c4cc;
      opacity: 0.7;
      right: 0;
      color: black;
      .active {
        color: #dc6018;
        background: rgba(252,145,83,.1);
      }
      ul {
        display: flex;
        flex-direction: column;
        li {
          width: 100%;
          line-height: 3rem;
          text-align: center;
        }
        li:nth-child(2) {
          border-top: 1px solid white
          border-bottom : 1px solid white
        }
      }
    }
    .content {
      display: flex;
      margin: 0 !important;
      justify-content: space-around;
      border-bottom: 1px solid #e7e6ee;
      background white;
      height 100%;
      > div {
        display: flex;
        flex-direction: column;
      }
    }
    .cube-page
      position: absolute
      z-index: 10
      top: 3.8em
      left: 0
      width: 100%
      height: 100%
      background: #efeff4
      .wrapper
        height: calc(100%)
        overflow-x: hidden
        overflow-y: auto
        // -webkit-overflow-scrolling: touch
        .desc
          padding: 10px
          margin: 10px 0
          line-height: 20px
          font-size: 14px
        .content
          margin: 10px
    .nav-scroll-list-wrap
      transform: rotate(0deg) // fix 子元素超出边框圆角部分不隐藏的问题
      position: relative
      background-color: white
      border-bottom : 1px solid rgba(0, 0, 0, 0.1)
      padding-right: 30px
      .cube-scroll-content
        display: inline-block
        .nav-wrapper
          display: inline-block
          white-space: nowrap
          line-height: 36px
          padding: 0 5px
          .nav-item
            display: inline-block
            padding: 0 5px
            &:nth-child(2)
              color: #fa7b7a
      .more-wrapper
        position: absolute
        right: 0
        top: 0
        bottom: 0
        z-index: 1
        background-color: #fff
        opacity: 0.95
        .more
          display: inline-block
          height: 1px
          width: 20px
          padding: 5px 0
          border: 1px solid #000
          border-right: transparent
          border-left: transparent
          background-color: #000
          background-clip: content-box
          margin: 11px
    .content-scroll-wrapper
      flex: 1
      position: relative
      .content-scroll-list-wrap
        width 100%
        height: 100%
        transform: rotate(0deg) // fix 子元素超出边框圆角部分不隐藏的问题
        position: absolute
        top: 0
        bottom: 0
        overflow: hidden
        .imgs-wrapper
          .imgs-item
            /*>img*/
            /*width: 100%*/
            .li-content {
              background-color white;
              padding: 0.5rem 0rem;
              display: flex;
              justify-content: space-around;
              border-bottom: 1px solid #e7e6ee;
              > div {
                display: flex;
                flex-direction: column;
              }
            }
    .cube-pulldown-wrapper
      text-align: center
      .before-trigger
        height: auto
        font-size: 30px
        align-self: flex-end
        span
          display: inline-block
          line-height: 1
          transition: all 0.3s
          color: #666
          padding: 15px 0
          &.rotate
            transform: rotate(180deg)
      .after-trigger
        flex: 1
        margin: 0
        .text-wrapper
          margin: 0 auto
          margin-top: 14px
          padding: 5px 0
          color: #498ec2
          background-color: #d6eaf8
        .cube-loading-spinners
          margin: auto
    .success-enter-active, .success-leave-active
      transition: width .5s
    .success-enter, .success-leave-to
      width: 70%
    .success-enter-to, .success-leave
      width: 100%
    .no-data {
      margin-top: 0.5em;
      font-weight: bold;
      color: #e31f1f;
      text-align: center;
    }
    .content-left {
      line-height: 4rem;
      font-weight: bold;
      font-size: 1.2rem;
      color: #007bff;
      align-items: center;
      flex-direction: column;
      width: 6em;
      display: flex;
      img {
        height: 3rem;
        width:3rem;
      }
      div {
        line-height: 2rem;
      }
      .doing {
        color: #efa42d;
      }
      .pass {
        color: #4eb54e;
      }
      .unpass {
        color: #de0d0d;
      }
    }
    .content-right {
      justify-content: space-around;
      width: 64%;
      > div {
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
      }
    }
    .hp-time {
      display: flex;
      justify-content: space-between;
    }
    .pop {
      width 4rem;
      background white
      li {
        line-height 1.2rem;
        text-align center;
        border-bottom 1px solid #dedede;
      }
      li:last-child {
        border none;
        color red;
      }
    }
    .back {
      position: fixed;
      top: 46%;
      background: rgba(0, 90, 255, 0.32);
      line-height: 2rem;
      margin-left: -4px;
      min-width: 4rem;
      color: white;
      border-bottom-right-radius: 8px;
      border-top-right-radius: 8px;
    }
</style>



