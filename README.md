<!--
author:   Philipp Wabnitz
version:  0.0.6
language: en
comment:  Just some LiaScript tests

script:
    https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js
    https://unpkg.com/@google/model-viewer/dist/model-viewer-legacy.js
    https://cdnjs.cloudflare.com/ajax/libs/processing.js/1.6.6/processing.min.js

@mv: <model-viewer src="@0" alt="@1" auto-rotate camera-controls></model-viewer>

import:
    https://raw.githubusercontent.com/LiaTemplates/mermaid_template/master/README.md
    https://raw.githubusercontent.com/LiaTemplates/processingjs/master/README.md
    https://raw.githubusercontent.com/LiaTemplates/aframe/master/README.md
    https://raw.githubusercontent.com/LiaTemplates/mec2/main/README.md
-->

# LiaTests

Just some tests with LiaScript.

Load the course: https://liascript.github.io/course/?https://raw.githubusercontent.com/pwab/LiaTests/main/README.md

## Iframe

### global

<iframe src="https://liascript.github.io"></iframe>

### local

<iframe src="https://pwab.github.io/LiaTests/web/index.html"></iframe>

## mermaidJS

Create some graphs.

``` @mermaid(2)
graph TD
A[Client] --> B[Load Balancer]
B --> C[Server01]
B --> D[Server02]
```

## model-viewer

Should really be added to the template repository.

@mv(https://modelviewer.dev/shared-assets/models/Astronaut.glb, A model of an astronaut)

[Astronaut](https://poly.google.com/view/dLHpzNdygsg) by [Poly](https://poly.google.com/user/4aEd8rQgKu2), licensed under [CC-BY](https://creativecommons.org/licenses/by/2.0/).

<model-viewer id="paused-change-demo" camera-controls autoplay animation-name="Running" ar shadow-intensity="1" src="https://modelviewer.dev/shared-assets/models/RobotExpressive.glb" alt="An animated 3D model of a robot"></model-viewer>
  <script>
  (() => {
    const modelViewer = document.querySelector('#paused-change-demo');

    self.setInterval(() => {
      modelViewer.animationName = modelViewer.animationName === 'Running' ?
        'Wave' : 'Running';
    }, 1500.0);
  })();
  </script>

[RobotExpressive](https://github.com/mrdoob/three.js/tree/dev/examples/models/gltf/RobotExpressive) by [Tomás Laulhé](https://www.patreon.com/quaternius), licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/). 


## A-Frame

In the manual of the template it is stated that it shouldn't be imported. Are there any advantages or disadvantages because of that?

<div style="height: 400px; width: 100%">
<a-scene embedded background="color: #ECECEC">
  <a-box position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9" shadow></a-box>
  <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E" shadow></a-sphere>
  <a-cylinder position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D" shadow></a-cylinder>
  <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4" shadow></a-plane>
</a-scene>
</div>

## ProcessingJS

Move the robot

```p5 -Roboterarm
float x, y;
float angle1 = 0.0;
float angle2 = 0.0;
float segLength = 100;

void setup() {
  size(640, 360);
  strokeWeight(30);
  stroke(255, 160);

  x = width * 0.3;
  y = height * 0.5;
}

void draw() {
  background(0);

  angle1 = (mouseX/float(width) - 0.5) * -2*PI;
  angle2 = (mouseY/float(height) - 0.5) * 2*PI;

  pushMatrix();
  segment(x, y, angle1);
  segment(segLength, 0, angle2);
  popMatrix();
}

void segment(float x, float y, float a) {
  translate(x, y);
  rotate(a);
  line(0, 0, segLength, 0);
}
```
@Processing.eval()

## mec2

Want to see some pendulums swing?

``` json @mec2
{
  "id":"chaos-pendulums",
  "gravity":true,
  "nodes": [
    { "id":"A0","x":200,"y":400,"base":true },
    { "id":"A1","x":280,"y":480,"m":2 },
    { "id":"B1","x":279,"y":481,"m":2 },
    { "id":"C1","x":278,"y":482,"m":2 },
    { "id":"D1","x":277,"y":483,"m":2 },
    { "id":"A2","x":360,"y":560,"m":3 },
    { "id":"B2","x":359,"y":561,"m":3 },
    { "id":"C2","x":358,"y":562,"m":3 },
    { "id":"D2","x":357,"y":563,"m":3 },
    { "id":"A3","x":440,"y":640,"m":4.7 },
    { "id":"B3","x":439,"y":641,"m":4.7 },
    { "id":"C3","x":438,"y":642,"m":4.7 },
    { "id":"D3","x":437,"y":643,"m":4.7 }
  ],
  "constraints": [
    { "id":"a1","p1":"A0","p2":"A1","len":{ "type":"const" } },
    { "id":"a2","p1":"A1","p2":"A2","len":{ "type":"const" } },
    { "id":"a3","p1":"A2","p2":"A3","len":{ "type":"const" } },
    { "id":"b1","p1":"A0","p2":"B1","len":{ "type":"const" } },
    { "id":"b2","p1":"B1","p2":"B2","len":{ "type":"const" } },
    { "id":"b3","p1":"B2","p2":"B3","len":{ "type":"const" } },
    { "id":"c1","p1":"A0","p2":"C1","len":{ "type":"const" } },
    { "id":"c2","p1":"C1","p2":"C2","len":{ "type":"const" } },
    { "id":"c3","p1":"C2","p2":"C3","len":{ "type":"const" } },
    { "id":"d1","p1":"A0","p2":"D1","len":{ "type":"const" } },
    { "id":"d2","p1":"D1","p2":"D2","len":{ "type":"const" } },
    { "id":"d3","p1":"D2","p2":"D3","len":{ "type":"const" } }
  ],
  "views": [
    { "show":"pos","of":"A3","as":"trace","id":"view1","stroke":"rgba(255,0,0,.5)" },
    { "show":"pos","of":"B3","as":"trace","id":"view2","stroke":"rgba(0,255,0,.5)" },
    { "show":"pos","of":"C3","as":"trace","id":"view3","stroke":"rgba(255,255,0,.5)" },
    { "show":"pos","of":"D3","as":"trace","id":"view4","stroke":"rgba(255,0,255,.5)" }
  ]
}
```

## eCharts

<script runOnce style="display: inline-block; width: 100%">
var option = {
    title: {
        text: '堆叠区域图'
    },
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'cross',
            label: {
                backgroundColor: '#6a7985'
            }
        }
    },
    legend: {
        data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎']
    },
    toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    xAxis: [
        {
            type: 'category',
            boundaryGap: false,
            data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        }
    ],
    yAxis: [
        {
            type: 'value'
        }
    ],
    series: [
        {
            name: '邮件营销',
            type: 'line',
            stack: '总量',
            areaStyle: {},
            emphasis: {
                focus: 'series'
            },
            data: [120, 132, 101, 134, 90, 230, 210]
        },
        {
            name: '联盟广告',
            type: 'line',
            stack: '总量',
            areaStyle: {},
            emphasis: {
                focus: 'series'
            },
            data: [220, 182, 191, 234, 290, 330, 310]
        },
        {
            name: '视频广告',
            type: 'line',
            stack: '总量',
            areaStyle: {},
            emphasis: {
                focus: 'series'
            },
            data: [150, 232, 201, 154, 190, 330, 410]
        },
        {
            name: '直接访问',
            type: 'line',
            stack: '总量',
            areaStyle: {},
            emphasis: {
                focus: 'series'
            },
            data: [320, 332, 301, 334, 390, 330, 320]
        },
        {
            name: '搜索引擎',
            type: 'line',
            stack: '总量',
            label: {
                show: true,
                position: 'top'
            },
            areaStyle: {},
            emphasis: {
                focus: 'series'
            },
            data: [820, 932, 901, 934, 1290, 1330, 1320]
        }
    ]
};

send.html(`<lia-chart option='${JSON.stringify(option)}'></lia-chart>`)

</script>
