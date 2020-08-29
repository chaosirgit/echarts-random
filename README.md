# echarts-random
This is an echarts random finance code
Copy the code to echarts example code area
```javascript
function needA(arr,j){
    return arr.filter(item => {
        return item.id !== j
    })
}
const dicArr = []
for (var i =0 ; i < 100 ; i ++){
    dicArr.push({id:i,value : 100})
}
let time = 1;
let people = dicArr.map(item => {return item.id});
let arr = dicArr.map(item=>{return item.value});
//input times to begin
const startTimes = 1


option = {
    title:{text:"随机财富规律",subtext:time},
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'cross',
            label: {
                backgroundColor: '#283b56'
            }
        },
        formatter:'序号:{b0}<br/>金额:{c0}'
    },
    legend: {
        data:['最新成交价', '预购队列']
    },
    xAxis: {
        name: '序号',
        type: 'category',
        data: people
    },
    yAxis: {
        name: '金额',
        type: 'value',
        axisLabel: {
                formatter: '{value}'
            }
    },
    series: [{
        data: arr,
        type: 'bar'
    }]
};
var timer = setInterval(function(){
    if (time >= startTimes){
        clearInterval(timer)
    }else{
        for(let j = 0;j < dicArr.length; j ++){
            //获得人的ID
            let point = Math.floor(Math.random()*99);

            //排除给的人
            var needArr = needA(dicArr,j) //max 98

            if (dicArr[j].value >= 1){
                dicArr[j].value -= 1
                dicArr[needArr[point].id].value += 1
            }
        }
        people = dicArr.map(item => {return item.id});
        arr = dicArr.map(item=>{return item.value});

        option.xAxis.data = people
        option.series[0].data = arr
        option.title.subtext = time
        myChart.setOption(option);
        time++
    }
},30);



```
