<template>
  <view>
    <view class="home_tab">
      <view class="home_tab_title">
        <view class="title_inner">
          <uni-segmented-control
            :current="current"
            :values="items.map(v => v.title)"
            @clickItem="onClickItem"
            styleType="text"
            activeColor="#e1397c"
            ></uni-segmented-control>
        </view>
        <view class="iconfont icon-search"></view>
      </view>
      <view class="home_content">
        <view v-if="current === 0">
          <home-recommend></home-recommend>
        </view>
        <view v-if="current === 1">
          <home-category></home-category>
        </view>
        <view v-if="current === 2">
          <home-new></home-new>
        </view>
        <view v-if="current === 3">
          <home-album></home-album>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
import homeRecommend from './home-recommend/index';
import homeCategory from './home-category/index';
import homeNew from './home-new/index';
import homeAlbum from './home-album/index';
import { uniSegmentedControl } from '@dcloudio/uni-ui'
export default {
  components: {
    homeRecommend,
    homeCategory,
    homeNew,
    homeAlbum,
    uniSegmentedControl
  },
  data () {
    return {
      current: 3,
      items: [
        {title: '推荐'},
        {title: '分类'},
        {title: '最新'},
        {title: '专辑'}
      ]
    }
  },
  methods: {
    onClickItem (e) {
      this.current = e.currentIndex
    }
  }
}
</script>

<style lang="scss">
  @import "./index.scss"
</style>