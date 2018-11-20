<div id="dv">
    <cspan>这是div中的第一个标签span标签</cspan>
    <p>这是div中的第二个标签p标签</p>
    <ul id="uu">哈哈
        <li>aa</li>
        <li>aabb</li>嘿嘿
        <li id="three">aabbcc</li>呵呵
        <li>aabbccdd</li>
        <li>aabbccddee</li>嘎嘎
    </ul>
</div>
<script>
    //十二行代码都是获取节点和元素的
    //ul
    var ulObj=my$("uu");
    //父级节点
    console.log(ulObj.parentNode);//DIV(id=dv)
    //父级元素
    console.log(ulObj.parentElement);//DIV(id=dv)
    //子节点
    console.log(ulObj.childNodes);//#text LI #text LI #text LI（id=three）#text LI #text LI #text
    //子元素
    console.log(ulObj.children);//LI LI LIi(id=three) LI LI
    console.log("---------------------------------------------------------");
    //第一个子节点------------------------------------------------------>IE8中获取的是子元素
    console.log(ulObj.firstChild);//哈哈
    //第一个子元素------------------------------------------------------>IE8中不支持
    console.log(ulObj.firstElementChild);//LI
    //最后一个子节点---------------------------------------------------->IE8中获取的是子元素
    console.log(ulObj.lastChild);//嘎嘎
    //最后一个子元素------------------------------------------------------>IE8中不支持
    console.log(ulObj.lastElementChild);//LI
    //某个元素的前一个兄弟结点-------------------------------------------->IE8中获取的是子元素
    console.log(my$("three").previousSibling);//嘿嘿
    //某个元素的前一个兄弟元素-------------------------------------------------->IE8中不支持
    console.log(my$("three").previousElementSibling);//LI
    //某个元素的后一个兄弟结点-------------------------------------------->IE8中获取的是子元素
    console.log(my$("three").nextSibling);//呵呵
    //某个元素的后一个兄弟元素-------------------------------------------------->IE8中不支持
    console.log(my$("three").nextElementSibling);//LI
</script>
