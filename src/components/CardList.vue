<template>
    <transition mode="out-in" :enter-active-class="enterActiveClass" appear>
        <div class="animated card-container" v-if="!loading">
            <div class="card" v-for="(item,index) in items">
                <div class="card-image">
                    <router-link :to="'/post/'+item.key">
                        <figure class="image">
                            <img :src="item.imageUrl | http2https" alt="Image">
                        </figure>
                    </router-link>
                </div>
                <div class="card-content">
                    <div class="media">
                        <div class="media-left">
                            <router-link class="authorname" :to="'/author/'+doubleBase64(item.authorname)">
                                <figure class="image is-48x48">
                                <img :src="item.avatar | http2https" alt="Image">
                                </figure>
                            </router-link>
                        </div>
                        <div class="media-content">
                            <p class="title is-5"> {{item.title}} </p>
                            <p class="subtitle is-6"></p>
                        </div>
                    </div>
                    <div class="content">
                        <router-link class="authorname" :to="'/author/'+doubleBase64(item.authorname)">
                        @{{item.authorname}}
                        </router-link>
                        <br>
                        <small>{{new Date(item.date) | formatDateTime}}</small>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
import { doubleBase64 } from '../filters'
export default {
  name: 'CardList',
  props: {
    items: Array,
    loading: Boolean,
    enterActiveClass: String
  },
  methods: {
    doubleBase64
  }
}
</script>
<style lang="scss">
@import '../scss/variable.scss';
.card-container {
  -webkit-column-count: 3;
  -webkit-column-gap: 15px;
  -webkit-column-rule: 5px solid #FFF;
  -webkit-column-width: 240px;

  -moz-column-count: 3;
  -moz-column-gap: 15px;
  -moz-column-rule: 5px solid #FFF;
  -moz-column-width: 240px;

  column-count: 3;
  column-gap: 15px;
  column-rule: 5px solid #FFF;
  column-width: 240px;

  .card {
    margin-bottom: 15px;
    -webkit-column-break-inside: avoid;
    page-break-inside: avoid;
    break-inside: avoid;
  }
}
</style>
