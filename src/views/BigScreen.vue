<template>
    <div class="bs">
        <div class="bs-header">
            <div class="bs-header-item"></div>
            <div class="bs-header-item"></div>
            <div class="bs-header-item right">
                <a @click="handleFullScreenClick"><icon type="md-expand"></icon></a>
            </div>
        </div>
        <div class="bs-body">
            <div class="bs-body-left">
                <div class="item"></div>
                <div class="item"></div>
                <div class="item"></div>
            </div>
            <div class="bs-body-center">
                <div class="item main" ref="map"></div>
                <div class="item"></div>
            </div>
            <div class="bs-body-right">
                <div class="item"></div>
                <div class="item"></div>
                <div class="item"></div>
            </div>
        </div>
    </div>
</template>

<script>
    import echarts from 'echarts'
    import 'echarts/map/js/china'
    // import 'echarts/map/js/province/guangdong'

    export default {
        name: "big-screen",
        data() {
            return {
                fullScreen: false,
            }
        },
        mounted() {



            let map = echarts.init(this.$refs['map'])
            map.setOption({
                backgroundColor: 'rgba(0,0,0,0)',//画布背景颜色
                geo: {
                    show: true,
                    map: 'china',
                    label: {
                        normal: {
                            show: false
                        },
                        emphasis: {
                            show: true,
                        }
                    },
                    roam: true,
                    itemStyle: {
                        normal: {
                            areaColor: '#031525',
                            borderWidth: 0,
                            shadowColor: 'rgba(255,0,0, 1)',
                            shadowBlur: 15
                        }
                    }
                },
                series: [
                    /*{
                        type: 'map',
                        map: 'china',
                        geoIndex: 1,
                        aspectScale: 0.75, //长宽比
                        showLegendSymbol: false, // 存在legend时显示
                        label: {
                            normal: {
                                show: true,
                            },
                            emphasis: {
                                show: false,
                                textStyle: {
                                    color: '#fff'
                                }
                            }
                        },
                        roam: false,
                        itemStyle: {
                            normal: {
                                areaColor: '#031525',
                                borderColor: '#3B5077',
                                borderWidth: 1
                            },
                            emphasis: {
                                areaColor: '#2B91B7'
                            }
                        },
                    },*/
                ]
            })
        },
        methods: {
            launchFullScreen(element) {
                if(element.requestFullScreen) {
                    element.requestFullScreen();
                } else if(element.mozRequestFullScreen) {
                    element.mozRequestFullScreen();
                } else if(element.webkitRequestFullScreen) {
                    element.webkitRequestFullScreen();
                }
            },
            exitFullscreen() {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.msExitFullscreen) {
                    document.msExitFullscreen();
                } else if (document.mozCancelFullScreen) {
                    document.mozCancelFullScreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                }
            },
            handleFullScreenClick() {
                this.fullScreen = !this.fullScreen
                if (this.fullScreen) {
                    this.launchFullScreen(document.querySelector('#app'))
                } else {
                    this.exitFullscreen()
                }
            }
        }
    }

    // Find the right method, call on correct element

</script>

<style lang="less">
    #app:-webkit-full-screen {
        width: 100%;
        height: 100%;
    }
    .bs {
        width: 100%;
        height: 100vh;
        overflow: hidden;
        display: flex;
        flex-direction: column;
        background-image: url("../assets/img/006.jpg");
        background-size: cover;

        &-header {
            height: 60px;
            padding: 0 32px;
            line-height: 60px;
            text-align: center;
            display: flex;

            &-item {
                flex: 1;
                &.left {
                    display: flex;
                    justify-content: flex-start;
                }
                &.center {
                    display: flex;
                    justify-content: center;
                }
                &.right {
                    display: flex;
                    justify-content: flex-end;
                }
            }
        }

        &-body {
            flex: 1;
            padding: 16px 32px;
            display: flex;

            &-left, &-right {
                flex: 0 0 30%;
                display: flex;
                flex-direction: column;

                & .item {
                    flex: 1;
                    background-color: rgba(255,255,255,.1);
                    margin-bottom: 16px;
                    border-radius: 4px;
                    &:last-child {
                        margin-bottom: 0;
                    }
                }

            }

            &-center {
                margin: 0 16px;
                flex: 1;
                display: flex;
                flex-direction: column;
                
                & .item {
                    background-color: rgba(255,255,255,.1);
                    flex: 1;
                    border-radius: 4px;
                    &.main {
                        background: transparent;
                        flex: 2;
                        margin-bottom: 16px;
                    }
                }
            }
        }
    }
</style>