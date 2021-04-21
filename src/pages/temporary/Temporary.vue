<template>
    <div class="temporary">
        <a-row >
            <a-col :span="5">
                <a-card :bordered="false">
<!--                    <a-card :bordered="true" style="width: 100%;height: 40px">-->
                        <!--        搜索框            -->
                        <a-input-search placeholder="搜索最近联系人、聊天记录" style="width:100%" @search="onSearch" />
                        <!--      Tabs切换栏位              -->
                    <a-tabs default-active-key="1" @change="callback" >
                        <a-tab-pane key="1" tab="会话">
                                <a-card>
<!--                            <div class="card-div">-->
<!--                                rgba(0, 0, 0, 0.65)-->
                               <span>最大接待：</span>
                                    <a-dropdown :trigger="['click']" >
                                        <a class="ant-dropdown-link" @click="e => e.preventDefault()">
                                            {{nowMenu}} <a-icon type="down" />
                                        </a>
                                        <a-menu slot="overlay" >
                                            <a-menu-item v-for="item in menuData"  :key="item" @click="menuItemClick(item)">
                                                <span v-text="item"></span>
                                            </a-menu-item>
                                        </a-menu>
                                    </a-dropdown>
                                <span>当前排队人数：</span>
                                <span>0</span>
<!--                            </div>-->
                                </a-card>
                            <!--    折风琴   -->
                            <a-collapse v-model="activeKey" style="border-radius: 0;border-top: none;opacity: 0.8;padding: 0 !important;">
                                <a-collapse-panel key="1" header="会话中" >
                                    <a-list item-layout="horizontal" :data-source="testdata"   style="width: 100%">
                                        <a-list-item slot="renderItem" slot-scope="item, index" :key="index">
                                            <a-list-item-meta
                                                    description="新订单消息"
                                            >
                                                <a slot="title" >{{item.title}}</a>
                                                <a-avatar
                                                        slot="avatar"
                                                        src="https://pic.netbian.com/uploads/allimg/210413/005834-161824671427be.jpg"
                                                        style="background: #13C2C2"
                                                />
                                            </a-list-item-meta>
                                        </a-list-item>
                                    </a-list>
                                </a-collapse-panel>
                                <a-collapse-panel key="2" header="会话结束"  >
<!--                                    <p>{{ text }}</p>-->
                                </a-collapse-panel>
                            </a-collapse>

                        </a-tab-pane>
                        <a-tab-pane key="2" tab="最近" force-render>
                            Content of Tab Pane 2
                        </a-tab-pane>
                        <a-tab-pane key="3" tab="星标">
                            Content of Tab Pane 3
                        </a-tab-pane>
                    </a-tabs>
<!--                    </a-card>-->
                </a-card>
            </a-col>
            <a-col :span="19" >
                <a-card :bordered="true" style="width: 100%;height: 835px">
<!--                    <div class="NoOrderClass">-->
<!--                        <img src="../../assets/small/order.png">-->
<!--                        <br/>-->
<!--                        <br/>-->
<!--                        <p>你还没有新的订单哦</p>-->
<!--                &lt;!&ndash;           路由跳转             &ndash;&gt;-->
<!--                        <a>点击查看更多订单</a>-->
<!--                    </div>-->
                    <a-card style="height: 80px;background: #409eff">
                        <div>
                            <a-avatar
                                    src="https://pic.netbian.com/uploads/allimg/210413/005834-161824671427be.jpg"
                                    style="display: inline-block;border: 1px solid #1890ff; "
                                    :size="50"
                            />
                            <a slot="title" style="font-size: 24px;margin-left: 10px;color: whitesmoke">fox miss you</a>
                        </div>
                    </a-card>
                    <!--          请求框        -->
<!--                    <a-list bordered="true">-->
<!--                        <RecycleScroller-->
<!--                                v-infinite-scroll="handleInfiniteOnLoad"-->
<!--                                style="height: 400px"-->
<!--                                :items="data"-->
<!--                                :item-size="73"-->
<!--                                key-field="email"-->
<!--                                :infinite-scroll-disabled="busy"-->
<!--                                :infinite-scroll-distance="10"-->
<!--                        >-->
<!--                            <a-list-item slot-scope="{ item }">-->
<!--                                <a-list-item-meta :description="item.email">-->
<!--                                    <a slot="title" :href="item.href">{{ item.name.last }}</a>-->
<!--                                    <a-avatar-->
<!--                                            slot="avatar"-->
<!--                                            src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"-->
<!--                                    />-->
<!--                                </a-list-item-meta>-->
<!--&lt;!&ndash;                                <div>Content {{ item.index }}</div>&ndash;&gt;-->
<!--                            </a-list-item>-->
<!--                        </RecycleScroller>-->
<!--                        <a-spin v-if="loading" class="demo-loading" />-->
<!--                    </a-list>-->
                    <a-card class="infinite-list-wrapper">
                        <chat/>
<!--                        <div class="infinite-list-wrapper" style="overflow:auto">-->
<!--                            <ul-->
<!--                                    class="list"-->
<!--                                    v-infinite-scroll="load"-->
<!--                                    infinite-scroll-disabled="disabled"-->
<!--                                    infinite-scroll-distance="100"-->
<!--                            >-->
<!--                                <li v-for="i in count" class="list-item" :key="i">{{ i }}</li>-->
<!--                            </ul>-->
<!--                            <p v-if="loading">加载中...</p>-->
<!--                            <p v-if="noMore">没有更多了</p>-->
<!--                        </div>-->
                    </a-card>
                </a-card>
            </a-col>

        </a-row>

    </div>
</template>

<script>
    // import reqwest from 'reqwest';
    import chat from './Chat'
    import infiniteScroll from 'vue-infinite-scroll';
    // import { RecycleScroller } from 'vue-virtual-scroller';
    // import 'vue-virtual-scroller/dist/vue-virtual-scroller.css';

    export default {
        name: "Temporary",
        directives: { infiniteScroll },
        components: {
            chat,
        },
        data() {
            return {
                count: 10,
                loading: false,
                busy: false,
                activeKey: ['1'],
                nowMenu:5,
                menuData:[5,10,100],
                testdata:[
                    {
                        title: '订单消息',
                    },
                    {
                        title: 'Ant Design Title 2',
                    },
                    {
                        title: 'Ant Design Title 3',
                    },
                    {
                        title: 'Ant Design Title 4',
                    },
                    {
                        title: 'Ant Design Title 2',
                    },
                    {
                        title: 'Ant Design Title 3',
                    },
                    {
                        title: 'Ant Design Title 4',
                    },
                ]
            };
        },
        computed: {
            noMore () {
                return this.count >= 20
            },
            disabled () {
                return this.loading || this.noMore
            }
        },
        methods: {
            //搜索框的方法
            onSearch(value) {
                console.log(value);
            },
            callback(key) {
                console.log(key);
            },
            // 人数选择下拉框
            handleChange(value) {
                console.log(`selected ${value}`);
            },
            menuItemClick (value) {
                this.nowMenu = value;
            },
            //折风琴事件
            // activeKey(key) {
            //     console.log(key);
            // },

            load () {
                this.loading = true
                setTimeout(() => {
                    this.count += 2
                    this.loading = false
                }, 2000)
            }

        },
    }
</script>

<style scoped>
    .temporary{
        width:100%;
        height: 100%;
    }

    .NoOrderClass{
        position: absolute;
        top: 50%;
        left: 50%;
        text-align: center;
    }
    .demo-loading {
        position: absolute;
        bottom: 40px;
        width: 100%;
        text-align: center;
    }
    .infinite-list-wrapper{
        height: 400px;
        width: 100%;
        border:1px solid red ;

    }
    /*.ant-collapse-content > .ant-collapse-content-box{*/
    /*    padding: 0 !important;*/
    /*}*/
    /*.card-div{*/
    /*    width: 100%;*/
    /*    height: 30px;*/
    /*    border: 1px solid  #d9d9d9;*/
    /*    line-height: 30px;*/
    /*    !*background: #d9d9d9;*!*/
    /*    text-indent: 5px;*/
    /*}*/

</style>
