SVG意为可缩放矢量图形，SVG使用XML格式定义图像
SVG使用XML来描述二维图形和绘图程序的语言，图像在放大或改变尺寸情况图像质量不会有损失

svg文件可通过标签嵌入到html文档：<embed>、<object>、<iframe>
    使用<embed>标签：
        优势：所有浏览器都支持，并允许使用脚本
        缺点：不推荐在HTML4和XHTML中使用
    语法：<embed src="circle.svg" type="image/svg+xml"/>
    
    使用<object>标签：
        优势：所有浏览器都支持
        缺点：不允许使用脚本
    语法：<object data="circle.svg" type="image/svg+xml"/></object>

    使用<iframe>标签：
        优势：所有浏览器都支持，并允许使用脚本
        缺点：不推荐在HTML4和XHTML中使用
    语法：<iframe src="circle.svg"></iframe>

直接在HTML嵌入SVG代码：
    <svg xmlns="http://www.w3.org/2000/svg" version="1.1">
        <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>
    </svg>

链接到SVG文件：
    <a href="circle.svg">View SVG file</a>

SVG Shape:
    矩形<rect>、圆形<circle>、椭圆<ellipse>、线<line>、折线<polyline>、多边形<polygon>、路径<path>
    矩形 - <rect>:
        <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width: 1;stroke:rgb(0,0,0)"/>
        width - 定义矩形的宽
        height - 定义矩形的高
        style - 定义css样式
        fiil属性定义矩形的填充色，
        stroke-width属性定义矩形边框的宽度，
        stroke属性定义矩形边框的颜色
        x，y属性定义矩形的坐标
        fill-opacity属性定义填充颜色透明度
        stroke-opacity属性定义轮廓颜色透明度
        opacity属性定义元素的透明度
        rx和ry属性可使矩形产生圆角
    
    圆形 - <circle>:
        <circle cx="40" cy="150" r="40" stroke="black" stroke-width="1" fill="red"/>
        cx和cy属性定义圆形的坐标
        r属性定义圆形的半径
    
    椭圆 - <ellipse>:
        <ellipse cx="105" cy="250" rx="100" ry="50" style="fill：yellow;stroke:purple;stroke-width:2"/>
        rx属性定义水平半轴的长度
        ry属性定义垂直半轴的长度

    线 - <line>:
        <line x1="0" y1="400" x2="100" y2="450" stroke="rgb(255,0,0)" stroke-width="2"/>
        x1和y1属性定义线的起始坐标
        x2和y2属性定义线的结束坐标
    
    多边形 - <polygon>:
        <polygon points="200,10 250,190 160,210" fill="lime" stroke="purple" stroke-width="1"/>
        points属性定义多边形每个角的x和y坐标
        fill-rule="evenodd"属性不填充

    折线 - <polyline>:
        <polyline points="20,20 40,25 60,40 80,120 120,40 200,180"
            fill="none" stroke="black" stroke-width="3"/>
        ponits属性定义每个点

    路径 - <path>:
        <path d="M150 0 L75 200 L225 200 Z"/>
        d属性用于定义路径
        M = moveto
        L = lineto
        H = horizontal lineto
        V = vertical lineto
        C = curveto
        S = smooth curveto
        Q - quadratic 
        T
        A
        Z = closepath

SVG文本 - <text>：
    <text x="0" y="15" fill="red">haha</text>

SVG Stroke属性：
    stroke属性：定义一条线，文本或元素的轮廓颜色
    stroke-width属性：定义一条线，文本或元素的轮廓厚度
    stroke-linecap属性：定义不同类型的开放路径的终结
    stroke-dasharry属性：用于创建虚线

SVG 滤镜：
    增加对SVG图形的特殊效果
    可用滤镜：
        feBlend - 与图像相结合的滤镜
        feColorMatrix - 用于彩色滤光片转换
        ...
    
SVG 模糊效果：
    <defs>标签定义短并含有特殊元素定义
    <filter>标签用来定义SVG滤镜，使用必须的id属性定义向图形应用那个滤镜
    <feGaussianBlur>：
        <defs>
            <filter id="f1" x="0" y="0">
                <feGaussianBlur in="SourceGraphic" stdDeviation="15"/>
            </filter>
        </defs>
        <rect width="90" height="90" stroke="green" stroke-width="3" fill="yellow" filter="url(#f1)"/>
    <filter>元素id属性定义一个滤镜的唯一名称
    <feGaussianBlur>元素定义模糊效果
    in="SourceGraphic" 定义由整个图像创建效果
    stdDeviation="15"定义模糊量

SVG 阴影：
    <feOffset>用于创建阴影效果
    
