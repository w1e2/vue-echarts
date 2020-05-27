<template>
    <div style="width: 100%;">
        <echartsLine :id="id1" :options="option1" :showFlag="true"></echartsLine>
        <echartsLine :id="id2" :options="option2" :showFlag="true"></echartsLine>
        <echartsLine :id="id3" :options="option3" :showFlag="true"></echartsLine>
        <div style="width:80%; margin-left:11%; margin-bottom: 50px;"> 
			<h3 style="text-align: left;">4、TOP10终端用户分布</h3>
            <!-- 也可以用element-ui实现 -->
			<div class="table">
				<div style="width: 60%;">
					<div class="header">
						<div class="item">序号</div>
						<div class="item">手机终端</div>
						<div class="item">用户数</div>
					</div>
					<div id="topId"></div>
				</div>
				<div style="width: 40%;">
					<echartsLine :id="id4" :options="option4" :showFlag="false"></echartsLine>
				</div>
			</div>
		</div>
    </div>
</template>

<script>
import echartsLine from '../components/Echarts-Line' // 只做了简单的组件封装，后续可进行优化
export default {
    components: { echartsLine },
    data() {
        return {
            option1: {},
            id1: 'main1', // id可以动态生成的-后续可改进  
            option2: {},
            id2: 'main2',
            option3: {},
            id3: 'main3',
            option4: {},
            id4: 'main4',
            arr: []
        }
    },
    mounted() {
        this.drawTable()
    },
    methods: {
        drawTable() {
            this.option1 = {
                title: {
                    text: '1、当日24小时流量趋势图',
                    textStyle: {
                        align: 'center',
                        color: '#000',
                        fontSize: 20,
                    },
                    top: '3%',
                    left: '10%',
                },
                tooltip: {
                    trigger: "axis",
                    axisPointer: {
                        type: "shadow",
                        label: {
                            show: true
                        }
                    }
                },
                legend: { // 图例
                    data: ["用户数", "流量(GB)"],
                    bottom: "10",
                    textStyle: {
                        color: "#000000"
                    }
                },
                xAxis: { // x轴
                    data: ['0时', '1时', '2时', '3时', '4时', '5时', '6时', '7时', '8时', '9时', '10时', '11时', '12时', '13时', '14时', '15时', '16时', '17时', '18时', '19时', '20时', '21时', '22时', '23时'],
                    type: 'category',
                    axisLine: {
                        show: true,
                        lineStyle: {
                            color: '#777777'
                        }
                    },
                    axisTick: {
                        show: true,
                    },
                    boundaryGap: true,
                },
                yAxis: [ // y轴
                    {
                        type: "value",
                        name: "流量(GB)",
                        nameTextStyle: {
                            color: "#000000"
                        },
                        position: "right",
                        splitLine: {
                            show: false
                        },
                        axisTick: {
                            show: true
                        },
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#000000'
                            }
                        },
                        axisLabel: {
                            show: true,
                            textStyle: {
                                color: "#000000"
                            }
                        }
                    },
                    {
                        type: "value",
                        name: "用户数",
                        nameTextStyle: {
                            color: "#000000"
                        },
                        splitLine: {
                            show: false
                        },
                        axisTick: {
                            show: true
                        },
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#000000'
                            }
                        },
                        axisLabel: {
                            show: true,
                            textStyle: {
                                color: "#000000"
                            }
                        },
                    },
                    {
                        type: "value",
                        gridIndex: 0,
                        min: 50,
                        max: 100,
                        splitNumber: 8,
                        splitLine: {
                            lineStyle: {
                                type: 'dotted',
                            }
                        },
                        axisLine: {
                            show: false
                        },
                        axisTick: {
                            show: false
                        },
                        axisLabel: {
                            show: false
                        },
                        splitArea: {
                            show: true,
                            areaStyle: {
                                color: ["rgba(250,250,250,0.0)", "rgba(250,250,250,0.05)"]
                            }
                        }
                    }
                ],
                dataZoom: [{ // 滑块
                        type: "slider", // 类型
                        xAxisIndex: 0, // 对应的轴 
                        bottom: "50", // 位置，定位 
                        start: 0, // 开始 
                        end: 70, // 结束 
                        handleIcon: "M0,0 v9.7h5 v-9.7h-5 Z",
                        handleStyle: { // 手柄的样式 
                            color: "#40bcf9",
                            borderColor: "#1fb2fb"
                        },
                        backgroundColor: "#e2f3ff", // 背景  
                        dataBackground: { // 数据背景 
                            lineStyle: {
                                color: "#000000"
                            },
                            areaStyle: {
                                color: "#d4d9dd"
                            }
                        },
                        fillerColor: "rgba(31,178,251,0.2)", // 被start和end遮住的背景 
                    }],
                    grid: { // 坐标系的位置（不包括滑块和图例）
                        left: '100',
                        right: '120',
                        bottom: '20%',
                        top: '18%',
                        containLabel: true,
                        borderWidth: '0'
                    },
                series: [{ // 数据展示样式
                        name: "用户数",
                        type: "line",
                        yAxisIndex: 1, // 使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
                        smooth: true, // 平滑曲线显示
                        showAllSymbol: true, // 显示所有图形。
                        symbol: "circle", // 标记的图形为实心圆
                        symbolSize: 10, // 标记的大小
                        itemStyle: {
                            // 折线拐点标志的样式
                            color: "#058cff"
                        },
                        lineStyle: {
                            color: "#058cff"
                        },
                        areaStyle:{
                            color: "rgba(5,140,255,0.2)" //面积样式
                        },
                        data: [424698, 292458, 239145, 216335, 213323, 268453, 481937, 779926, 979604, 1001045, 980206, 1022262, 1078375, 1000971, 970579, 982419,1015188, 1071194, 1073642, 997670, 933345, 835561, 749460, 604010],
                    },
                    {
                        name: "流量(GB)",
                        type: "bar",
                        barWidth: 15,
                        itemStyle: {
                            color: "#20d180"
                        },
                        data: [1153.199515, 525.6687154, 297.9072017, 234.9259967, 235.3401274, 403.527691, 896.5818437, 1808.769185, 2398.814451, 2428.226149, 2490.74319, 2286.962027, 2423.526401, 2217.75643, 2253.688007, 2259.717199, 2204.200084, 2153.108417, 2177.084424, 2196.133044, 2364.866589, 2390.015792, 2234.462158, 1700.479724],
                    }
                ]
            };

            let index = 0;
            let colorList = ['#f36c6c', '#e6cf4e', '#20d180', '#0093ff'];
            this.option2 = {
                title: {
                    text: '2、TOP10应用',
                    textStyle: {
                        align: 'center',
                        color: '#000',
                        fontSize: 20,
                    },
                    top: '3%',
                    left: '10%',
                },
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {
                        type: 'shadow'
                    },
                },
                legend: {
                    show: false
                },
                grid: {
                    left: '35',
                    right: '50',
                    bottom: '20',
                    containLabel: true,
                    borderWidth: '0'
                },
                xAxis: {
                    type: 'value',
                    splitLine: {
                        show: false
                    },
                    axisLabel: {
                        show: false
                    },
                    axisTick: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    }
                },
                yAxis: {
                    type: 'category',
                    inverse: true, // true为降序，false为升序
                    axisLine: {
                        show: false
                    },
                    axisTick: {
                        show: false
                    },
                    axisPointer: {
                        label: {
                            show: false,
                            margin: 30
                        }
                    },
                    data: ['快手', '爱奇艺', '今日头条', '微信', '腾讯网', '腾讯视频', '苹果应用商城', '天翼视讯', 'cibn互联网电视', '朋友圈', '王者荣耀'],
                    axisLabel: {
                        margin: 150,
                        fontSize: 14,
                        align: 'left',
                        color: '#333',
                        rich: {
                            a1: {
                                color: '#fff',
                                backgroundColor: colorList[0],
                                width: 30,
                                height: 30,
                                align: 'center',
                                borderRadius: 2
                            },
                            a2: {
                                color: '#fff',
                                backgroundColor: colorList[1],
                                width: 30,
                                height: 30,
                                align: 'center',
                                borderRadius: 2
                            },
                            a3: {
                                color: '#fff',
                                backgroundColor: colorList[2],
                                width: 30,
                                height: 30,
                                align: 'center',
                                borderRadius: 2
                            },
                            b: {
                                color: '#fff',
                                backgroundColor: colorList[3],
                                width: 30,
                                height: 30,
                                align: 'center',
                                borderRadius: 2
                            }
                        },
                        formatter: function(params) {
                            if (index == 11) {
                                index = 0;
                            }
                            index++;
                            if (index - 1 < 3) {
                                return [
                                    '{a' + index + '|' + index + '}' + '  ' + params
                                ].join('\n')
                            } else {
                                return [
                                    '{b|' + index + '}' + '  ' + params
                                ].join('\n')
                            }
                        }
                    }
                },
                series: [{
                        z: 2,
                        name: '流量',
                        type: 'bar',
                        data: [25190.68614,15991.71338,13286.59763,12806.02477,8956.905566,8707.45519,6244.248559,5960.895255,5742.49801,5512.997867,3086.518552].map((item, i) => {
                            let itemStyle = {
                                color: i > 3 ? colorList[3] : colorList[i]
                            }
                            return {
                                value: item,
                                itemStyle: itemStyle
                            };
                        }),
                        label: {
                            show: true,
                            position: 'right',
                            color: '#333333',
                            fontSize: 14,
                            offset: [10, 0]
                        }
                    }

                ]
            };

            this.option3 = {
                title: {
                    text: '3、实时流量及人数展示（1小时自动刷新）',
                    textStyle: {
                        align: 'center',
                        color: '#000',
                        fontSize: 20,
                    },
                    top: '3%',
                    left: '10%',
                },
                tooltip: {
                    trigger: "axis",
                    axisPointer: {
                        type: "shadow",
                        label: {
                            show: true
                        }
                    }
                },
                legend: {
                    data: ["用户数", "流量(GB)"],
                    bottom: "10",
                    textStyle: {
                        color: "#000000"
                    }
                },
                xAxis: {
                    data: ['1时', '2时', '3时', '4时', '5时', '6时', '7时', '8时', '9时', '10时', '11时'],
                    type: 'category',
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#777777'
                            }
                        },
                        axisTick: {
                            show: false,
                        },
                        boundaryGap: true,
                },
                yAxis: [
                    {
                        type: "value",
                        name: "流量(GB)",
                        nameTextStyle: {
                            color: "#000000"
                        },
                        position: "right",
                        splitLine: {
                            show: false
                        },
                        axisTick: {
                            show: true
                        },
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#000000'
                            }
                        },
                        axisLabel: {
                            show: true,
                            textStyle: {
                                color: "#000000"
                            }
                        }
                    },
                    {
                        type: "value",
                        name: "用户数",
                        nameTextStyle: {
                            color: "#000000"
                        },
                        splitLine: {
                            show: false
                        },
                        axisTick: {
                            show: true
                        },
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#000000'
                            }
                        },
                        axisLabel: {
                            show: true,
                            textStyle: {
                                color: "#000000"
                            }
                        },
                    },
                    {
                        type: "value",
                        gridIndex: 0,
                        min: 50,
                        max: 100,
                        splitNumber: 8,
                        splitLine: {
                            lineStyle: {
                                type: 'dotted',
                            }
                        },
                        axisLine: {
                            show: false
                        },
                        axisTick: {
                            show: false
                        },
                        axisLabel: {
                            show: false
                        },
                        splitArea: {
                            show: true,
                            areaStyle: {
                                color: ["rgba(250,250,250,0.0)", "rgba(250,250,250,0.05)"]
                            }
                        }
                    }
                ],
                dataZoom: [{
                        type: "slider", // 类型 
                        xAxisIndex: 0, // 对应的轴 
                        bottom: "50", // 位置，定位 
                        start: 30, // 开始 
                        end: 100, // 结束 
                        handleIcon: "M0,0 v9.7h5 v-9.7h-5 Z",
                        handleStyle: { // 手柄的样式 
                            color: "#40bcf9",
                            borderColor: "#1fb2fb"
                        },
                        backgroundColor: "#e2f3ff", // 背景  
                        dataBackground: { // 数据背景 
                            lineStyle: {
                                color: "#000000"
                            },
                            areaStyle: {
                                color: "#d4d9dd"
                            }
                        },
                        fillerColor: "rgba(31,178,251,0.2)", // 被start和end遮住的背景 
                    }],
                    grid: {
                        left: '100',
                        right: '120',
                        bottom: '20%',
                        top: '18%',
                        containLabel: true,
                        borderWidth: '0'
                    },
                series: [
                    {
                        name: "用户数",
                        type: "line",
                        yAxisIndex: 1, //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
                        smooth: true, //平滑曲线显示
                        showAllSymbol: true, //显示所有图形。
                        symbol: "circle", //标记的图形为实心圆
                        symbolSize: 10, //标记的大小
                        itemStyle: {
                            //折线拐点标志的样式
                            color: "#058cff"
                        },
                        lineStyle: {
                            color: "#058cff"
                        },
                        areaStyle:{
                            color: "rgba(5,140,255,0.2)" //面积样式
                        },
                        data: [986206, 1041045, 978604, 772926, 483937, 269453, 218323, 215335, 639145, 792458, 824698,],
                    },
                    {
                        name: "流量(GB)",
                        type: "bar",
                        barWidth: 15,
                        itemStyle: {
                            color: "#20d180"
                        },
                        data: [12490.74319, 12428.226149, 32398.814451, 91808.769185, 8896.5818437, 7403.527691, 6235.3401274, 5234.9259967, 3297.9072017, 5525.6687154, 4153.199515 ],
                    }
                ]
            };

            // 实现1小时刷新数据功能
            // let _this = this
            // let timer = setInterval(()=>{
            //     axios.get(url,(res)=>{
            //         // TODO 返回结果的判断
            //         ...
            //         _this.option3.series.push(res) // 前后端约定好数据格式，修改option3.series里的data数据或者option3.series
            //         setTimeout(fun, 0) // 防止页面卡死
            //     })
            // },3600000)

            this.arr = [ // 可通过请求后端返回需要的数据
                {'mobileTerminal': '华为', 'usageAmount': '843435'},
                {'mobileTerminal': '苹果', 'usageAmount': '479120'},
                {'mobileTerminal': 'vivo', 'usageAmount': '259875'},
                {'mobileTerminal': 'oppo', 'usageAmount': '198667'},
                {'mobileTerminal': '小米', 'usageAmount': '195255'},
                {'mobileTerminal': '三星', 'usageAmount': '60524'},
                {'mobileTerminal': '乐视', 'usageAmount': '19429'},
                {'mobileTerminal': '魅族', 'usageAmount': '19335'},
                {'mobileTerminal': '一加', 'usageAmount': '13184'},
                {'mobileTerminal': '世纪天元', 'usageAmount': '7359'}
            ];

            let arrStr = '';
            this.arr.forEach((e, index) => {
                if (index%2 === 0) {
                    arrStr += `<div class="list">
                                <div class="list_left">${index + 1}</div>
                                <div class="list_center">${e.mobileTerminal}</div>
                                <div class="list_right">${e.usageAmount}</div>
                            </div>`
                } else {
                    arrStr += `<div class="list1">
                                <div class="list_left">${index + 1}</div>
                                <div class="list_center">${e.mobileTerminal}</div>
                                <div class="list_right">${e.usageAmount}</div>
                            </div>`
                }
            })
            // console.log(arrStr)

            // 拼接完字符串数组后用innerHTML把它渲染到页面中
            document.getElementById("topId").innerHTML = arrStr;
            this.option4 = {
                color: ['#ff9f7f','#fb7293','#37a2da','#32c5e9','#9fe6b8','#ffdb5c','#ff9f7f','#fb7293','#e7bcf3','#8378ea'],
                tooltip : {
                    trigger: 'item',
                    formatter: "手机终端：{b}<br/> 用户数：{c}<br/> 用户占比：{d}%"
                },
                toolbox: {
                    show : true
                },
                series : [
                    {
                        name:'',
                        type:'pie',
                        radius : [0, 120],
                        data:[
                            {'name': '华为', 'value': '843435'},
                            {'name': '苹果', 'value': '479120'},
                            {'name': 'vivo', 'value': '259875'},
                            {'name': 'oppo', 'value': '198667'},
                            {'name': '小米', 'value': '195255'},
                            {'name': '三星', 'value': '60524'},
                            {'name': '乐视', 'value': '19429'},
                            {'name': '魅族', 'value': '19335'},
                            {'name': '一加', 'value': '13184'},
                            {'name': '世纪天元', 'value': '7359'},
                        ]
                    }
                ],
            };
        }
    },
}
</script>

<style>
.main {
	width: 100%; 
	height: 500px;
}

.echarts-container{
  width: 100%;
  height: 20rem;
}
.item {
    width: 100%;
    height: 30px;
    justify-content: center;
    display: flex;
    align-items: center;
    font-size: 16px;
    text-align: center
}

.header {
    display: flex;
    font-size: 14px;
    width: 100%;
    justify-content: space-around;
	background-color: #0199FF; 
	color: white
}
.table {
	width:100%; 
    height: 330px;
	display: flex; 
	align-items: center;
	margin-left: 10px;
}

.list {
	display: flex; 
	text-align: center; 
	align-items: center; 
	justify-content: space-around; 
	height: 30px;
	background-color: rgba(230, 230, 230, 0.5);
}
.list1 {
	display: flex; 
	text-align: center; 
	align-items: center; 
	justify-content: space-around; 
	height: 30px;
	background-color: rgba(250, 250, 250, 0.5);
}

.list_left {
	font-size: 15px; 
	line-height: 30px; 
	width: 30%;
}

.list_center {
	font-size: 15px; 
	line-height: 30px; 
	padding-bottom: 3px; 
	width: 30%
}

.list_right {
	font-size: 15px; 
	line-height: 30px; 
	padding-bottom: 3px; 
	width: 18%; 
	text-align: right; 
	padding-right: 12%
}
</style>