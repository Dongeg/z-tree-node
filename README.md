# zTree v3.5笔记

### 基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" href="../zTree_v3-master/css/zTreeStyle/zTreeStyle.css">
</head>
<body>
    <ul id="tree" class="ztree">
    </ul>
    <script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>
    <script src="../zTree_v3-master/js/jquery.ztree.core.js"></script>
    <script>
    var zTree;
    //配置
    var setting = {
        view: {
            dblClickExpand: false,
            showLine: true,
            selectedMulti: false
        },
        data: {
            simpleData: {
                enable: true,
                idKey: "id",
                pIdKey: "pId",
                rootPId: ""
            }
        },
        callback: {
            beforeClick: function(treeId, treeNode) {
                var zTree = $.fn.zTree.getZTreeObj("tree");
                if (treeNode.isParent) {
                    zTree.expandNode(treeNode);
                    return false;
                } else {
                    demoIframe.attr("src", treeNode.file + ".html");
                    return true;
                }
            }
        }
    };
    //模拟数据
    var zNodes = [
        { 
        	id: 1,
        	pId: 0, 
        	name: "[core] 基本功能 演示", 
        	open: true 
        },
        { 
        	id: 101, 
        	pId: 1, 
        	name: "最简单的树 --  标准 JSON 数据", 
        	file: "core/standardData" },

        { 
        	id: 2, pId: 0,
        	name: "[excheck] 复/单选框功能 演示", 
        	open: false 
        },

        { 
        	id: 208, 
        	pId: 2, 
        	name: "Checkbox halfCheck 演示", 
        	file: "excheck/checkbox_halfCheck" 
        },
        { 
        	id: 202, 
        	pId: 2, 
        	name: "Checkbox 勾选统计", 
        	file: "excheck/checkbox_count" 
        },

    ];
    //初始化
    $(document).ready(function() {
        var t = $("#tree");
        t = $.fn.zTree.init(t, setting, zNodes);
    });
    </script>
</body>
</html>
```

### 学习心得

z-tree的文档写的不是很好，一开始看的时候一头雾水，直接看demo源码能快速理解它的大体架构，再去看demo上的介绍和api会比较容易上手

要使用一些高级功能要引入专门的js文件

