<template>
    <div style="height:100%" v-if="URL">
        <div id="spinner" v-if="showSpinner">
            <div id="spinner-parent">
                <div class="spinner-double-bounce-bounce2"></div>
                <div class="spinner-double-bounce-bounce1"></div>
            </div>
        </div>
        <mt-loadmore v-else :autoFill="false" :bottomDistance="70" :top-method="loadTop" :bottom-method="loadBottom" :top-all-loaded="topAllLoaded" :bottom-all-loaded="bottomAllLoaded" :bottomPullText="`上拉加载更多`" :bottomDropText="`释放加载更多`" ref="loadMore">
            <div v-if="nothing && !showSpinner" :style="{'margin-top': offsetTop || 0}" :class="$style.nothing">
                <img :src="nothingImg" alt="空空如也">
            </div>
            <ul v-else style="background-color: #fff">
                <FindPersonItem v-for="(item, index) in dataList" :key="index" :item="item"></FindPersonItem>
            </ul>
            <div v-show="bottomAllLoaded && !nothing" :class="$style.bottmAll">没有更多了</div>
        </mt-loadmore>
    </div>
</template>
<script>
import request, { createAPI, addAccessToken } from '../../utils/request';
import FindPersonItem from './FindPersonItem';

if(typeof String.prototype.endsWith != 'function') {
    String.prototype.endsWith = function(suffix) {
        return this.indexOf(suffix, this.length - suffix.length) !== -1;
    };
}
const LoadMore = {
    name: "LoadMore",
    props: ["nothingImg", "URL", "offsetTop"],
    data: () => ({
        formateURL: "",
        dataList: [],
        showSpinner: false,
        bottomStatus: "",
        topAllLoaded: false,
        bottomAllLoaded: false,
    }),
    components:{
        FindPersonItem
    },
    methods: {
        loadData(merge) {
            let offset = merge ? this.dataList.length : 0;
            let params = {
                limit: 10,
                offset,
            };
            if(this.formateURL) {
                request.get(createAPI(this.formateURL), { params })
                    .then(({ data = [] }) => {
                        this.showSpinner = false;
                        this.bottomAllLoaded = data.length < params.limit ? !0 : !1;
                        this.dataList = merge ? Array.from(new Set([...this.dataList, ...data])) : [...data];
                    })
                    .catch(error => {
                        this.dataList = [];
                        this.showSpinner = false;
                        this.bottomAllLoaded = true;
                    });
            } else {
                this.dataList = [];
                this.showSpinner = false;
                this.bottomAllLoaded = true;
            }
        },
        loadTop() {
            // 上拉刷新
            this.loadData();
            // 延时隐藏
            setTimeout(() => {
                this.$refs.loadMore.onTopLoaded();
            }, 700);
        },
        loadBottom() {
            // 下拉加载
            this.loadData(true);
            // 延时隐藏
            setTimeout(() => {
                this.$refs.loadMore.onBottomLoaded();
            }, 700);
        }
    },

    computed: {
        nothing() {
            return !(this.dataList.length);
        },
    },
    watch: {
        URL(val) {
            this.formateURL = val.endsWith("name=") ? "locations/hots" : val;
            this.showSpinner = true;
            this.loadData();
        }
    },
    created() {
        if(this.URL) {
            this.formateURL = this.URL.endsWith("name=") ? "locations/hots" : this.URL;
            this.dataList = [];
            this.offset = 0;
            this.showSpinner = true;
            this.loadData();
        }
    }
}

export default LoadMore;
</script>
<style lang="less" module>
.nothing {
    width: 100%;
    display: flex;
    font-size: 24px;
    align-items: center;
    justify-content: center;
    text-align: center;
    height: 100vh;
    color: #ccc;
    background-color: #fff;
    >img {
        margin: 30%;
        width: 70%;
    }
}

.bottmAll {
    width: 100%;
    height: 40px;
    font-size: 14px;
    line-height: 40px;
    text-align: center;
}
</style>