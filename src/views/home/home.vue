<style lang="less">
    @import "./home.less";
    @import "../../styles/common.less";
</style>
<template>
    <div class="home-main">
        <Row :gutter="10">
            <Col :md="12" :lg="8" :style="{marginBottom: '10px'}">
                <Card>
                    <Row type="flex" class="user-infor">
                        <Col span="8">
                        <Row class-name="made-child-con-middle" type="flex" align="middle">
                            <img class="avator-img" :src="avatorPath"/>
                        </Row>
                        </Col>
                        <Col span="16" style="padding-left:6px;">
                        <Row class-name="made-child-con-middle" type="flex" align="middle">
                            <div>
                                <b class="card-user-infor-name">{{ userInfo.userName }}</b>
                                <p>{{ userInfo.name }}</p>
                            </div>
                        </Row>
                        </Col>
                    </Row>
                    <div class="line-gray"></div>
                    <Row class="margin-top-8">
                        <Col span="8">
                        <p class="notwrap">上次登录时间:</p></Col>
                        <Col span="16" class="padding-left-8" v-if="userInfo.lastTime">
                        {{ userInfo.lastTime | formatDate }}
                        </Col>
                        <Col span="16" class="padding-left-8" v-else>
                        —
                        </Col>
                    </Row>
                    <Row class="margin-top-8">
                        <Col span="8">
                        <p class="notwrap">上次登录IP:</p></Col>
                        <Col span="16" class="padding-left-8">
                        {{ userInfo.lastIp || '—' }}</Col>
                    </Row>
                </Card>
            </Col>
            <Col :md="12" :lg="16" :style="{marginBottom: '10px'}">
                <Card>
                    <p slot="title" class="card-title">
                        <Icon type="android-checkbox-outline"></Icon>
                        待执行任务
                    </p>
                    <div class="to-do-list-con">
                        <template v-if="toDoList.length">
                            <div v-for="(item, index) in toDoList" :key="index" class="to-do-item">
                                <to-do-list-item :content="item.title"></to-do-list-item>
                            </div>
                        </template>
                        <p v-else style="text-align: center;line-height: 145px;">暂无数据</p>
                    </div>
                </Card>
            </Col>
            <Col>
                <Row :gutter="5">
                    <Col :xs="24" :sm="12" :md="6" :style="{marginBottom: '10px'}">
                    <infor-card
                            id-name="user_created_count"
                            :end-val="count.createUser"
                            iconType="android-person"
                            color="#2d8cf0"
                            intro-text="管理员数量"
                    ></infor-card>
                    </Col>
                    <Col :xs="24" :sm="12" :md="6" :style="{marginBottom: '10px'}">
                    <infor-card
                            id-name="visit_count"
                            :end-val="count.visit"
                            iconType="android-cloud"
                            color="#64d572"
                            :iconSize="50"
                            intro-text="手机号数量"
                    ></infor-card>
                    </Col>
                    <Col :xs="24" :sm="12" :md="6" :style="{marginBottom: '10px'}">
                    <infor-card
                            id-name="collection_count"
                            :end-val="count.collection"
                            iconType="upload"
                            color="#ffd572"
                            intro-text="今日数据采集量"
                    ></infor-card>
                    </Col>
                    <Col :xs="24" :sm="12" :md="6" :style="{marginBottom: '10px'}">
                    <infor-card
                            id-name="transfer_count"
                            :end-val="count.transfer"
                            iconType="shuffle"
                            color="#f25e43"
                            intro-text="今日服务调用量"
                    ></infor-card>
                    </Col>
                </Row>
                <Row>
                    <Card :padding="0">
                        <p slot="title" class="card-title">
                            <Icon type="map"></Icon>
                            今日服务调用分布
                        </p>
                        <div class="map-con">
                            <Col span="10">
                                <map-data-table :cityData="cityData" height="281"
                                            :style-obj="{margin: '12px 0 0 11px'}"></map-data-table>
                            </Col>
                            <Col span="14" class="map-incon">
                                <!--<Row type="flex" justify="center" align="middle">-->
                                    <data-source-pie></data-source-pie>
                                    <!--<home-map :city-data="cityData"></home-map>-->
                                <!--</Row>-->
                            </Col>
                        </div>
                    </Card>
                </Row>
            </Col>
        </Row>
        <!--<Row :gutter="10" class="margin-top-10">-->
            <!--<Col :md="24" :lg="8" :style="{marginBottom: '10px'}">-->
            <!--<Card>-->
                <!--<p slot="title" class="card-title">-->
                    <!--<Icon type="android-map"></Icon>-->
                    <!--上周每日数据采集统计-->
                <!--</p>-->
                <!--<div class="data-source-row">-->
                    <!--<visite-volume></visite-volume>-->
                <!--</div>-->
            <!--</Card>-->
            <!--</Col>-->
            <!--<Col :md="24" :lg="8" :style="{marginBottom: '10px'}">-->
            <!--<Card>-->
                <!--<p slot="title" class="card-title">-->
                    <!--<Icon type="ios-pulse-strong"></Icon>-->
                    <!--数据来源统计-->
                <!--</p>-->
                <!--<div class="data-source-row">-->
                    <!--<data-source-pie></data-source-pie>-->
                <!--</div>-->
            <!--</Card>-->
            <!--</Col>-->
            <!--<Col :md="24" :lg="8">-->
            <!--<Card>-->
                <!--<p slot="title" class="card-title">-->
                    <!--<Icon type="android-wifi"></Icon>-->
                    <!--各类变化统计-->
                <!--</p>-->
                <!--<div class="data-source-row">-->
                    <!--<user-flow></user-flow>-->
                <!--</div>-->
            <!--</Card>-->
            <!--</Col>-->
        <!--</Row>-->
        <!--<Row class="margin-top-10">-->
            <!--<Card>-->
                <!--<p slot="title" class="card-title">-->
                    <!--<Icon type="ios-shuffle-strong"></Icon>-->
                    <!--上周每日服务调用量-->
                <!--</p>-->
                <!--<div class="line-chart-con">-->
                    <!--<service-requests></service-requests>-->
                <!--</div>-->
            <!--</Card>-->
        <!--</Row>-->
    </div>
</template>

<script>
    import cityData from './map-data/get-city-value.js';
    import homeMap from './components/map.vue';
    import dataSourcePie from './components/dataSourcePie.vue';
    import visiteVolume from './components/visiteVolume.vue';
    import serviceRequests from './components/serviceRequests.vue';
    import userFlow from './components/userFlow.vue';
    import countUp from './components/countUp.vue';
    import inforCard from './components/inforCard.vue';
    import mapDataTable from './components/mapDataTable.vue';
    import toDoListItem from './components/toDoListItem.vue';

    export default {
        name: 'home',
        components: {
            homeMap,
            dataSourcePie,
            visiteVolume,
            serviceRequests,
            userFlow,
            countUp,
            inforCard,
            mapDataTable,
            toDoListItem
        },
        data () {
            return {
                userInfo: {},
                toDoList: [
                    // {
                    //     title: '去iView官网学习完整的iView组件'
                    // },
                    // {
                    //     title: '去iView官网学习完整的iView组件'
                    // },
                    // {
                    //     title: '去iView官网学习完整的iView组件'
                    // },
                    // {
                    //     title: '去iView官网学习完整的iView组件'
                    // },
                    // {
                    //     title: '去iView官网学习完整的iView组件'
                    // }
                ],
                count: {
                    createUser: 496,
                    visit: 3264,
                    collection: 24389305,
                    transfer: 39503498
                },
                cityData: cityData,
                showAddNewTodo: false,
                newToDoItemValue: ''
            };
        },
        computed: {
            avatorPath () {
                return localStorage.avatorImgPath;
            }
        },
        methods: {
            init () {
                this.userInfo = this.$store.state.user.info;
            }
        },
        created () {
            this.init();
        }
    };
</script>
