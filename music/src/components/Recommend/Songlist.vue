<template>
    <div class="song">
        <div class="song-top">
           <h3>最新音乐</h3>
        </div>
        <ul class="song-list">
            <li v-for="value in newsong" :key="value.id" class="item" @click="selectMusic(value.id)">
                <!--<img :src="value.picUrl" alt="">-->
                <img v-lazy="value.picUrl" alt="">
                <div>
                    <h3>{{value.name}}</h3>
                    <p>{{value.song.artists[0].name}} </p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'Songlist',
  props: {
    newsong: {
      type: Array,
      default: () => [],
      require: true
    }
  },
  methods: {
    ...mapActions([
      'setFullScreen',
      'setShowMiniPlayer',
      'setSongDetail'
    ]),
    selectMusic (id) {
      this.setFullScreen(true)
      this.setShowMiniPlayer(false)
      this.setSongDetail([id])
    }
  }
}
</script>

<style scoped lang="scss">
    @import "../../assets/css/mixin";
    @import "../../assets/css/variable";
.song{
    width: 100%;
    @include bg_sub_color();
    .song-top{
        width: 100%;
        height: 84px;
        line-height: 84px;
        border-bottom: 1px solid #ccc;
        @include bg-sub_color();
        h3{
            @include font_size($font_large);
            font-weight: bold;
            @include font_color();
        }
    }
    .song-list{
        width: 100%;
        /* 清除浮动*/
        overflow: hidden;
        .item{
            width: 100%;
            height: 200px;
            display: flex;
            align-items: center;
            padding: 0 20px;
            margin-bottom: 20px;
            border-bottom: 1px solid #ccc;
            img{
                width: 150px;
                height: 150px;
                border-radius: 20px;
                margin-right: 20px;
            }
            div{
                h3{
                    @include font_size($font_large);
                    @include font_color();
                }
                p{
                    @include font_size($font_small);
                    @include font_color();
                    margin-top: 20px;
                    opacity: 0.6;
                }
            }
        }
    }
}
</style>
