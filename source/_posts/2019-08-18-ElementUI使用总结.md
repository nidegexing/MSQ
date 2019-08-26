---
title: ElementUI使用总结
date: 2019-08-18 22:03:45
categories:
- 光鲜的前端
- VUE
tags:
- VUE
---
总结ElementUI使用中的笔记。

<!--more-->

# Table
1 表格三重奏
发明者为可爱的杨波同学，我记录下。
```
<el-table-column
    type="index"
    width="60"
    align="center"
    fixed
    label="SEARCH"
>
    <template slot="header" slot-scope="scope">
        <div class="docker-search-icon" @click="postData">
            <i class="el-icon-loading" v-if="loading"/>
            <i class="el-icon-search" v-else/>
        </div>
    </template>
    <el-table-column
        type="index"
        width="60"
        align="center"
        fixed
        label="SEARCH"
    >
        <template slot="header" slot-scope="scope">
            <div class="docker-search-icon" @click="cleanCondition">
                清空条件
            </div>
        </template>
        <template slot-scope="{row}">
            <div class="absolute-full">
                <div>1</div>
            </div>
        </template>
    </el-table-column>
</el-table-column>
```
2 拖动
Table拖动：https://blog.csdn.net/qq_26440803/article/details/83663511
VUE中使用DOM：https://www.jianshu.com/p/d92b9efe3e6a
SortAble：https://github.com/SortableJS/Sortable
```
    //td-->cell拖拽
    addDrop() {
        console.log("addDrop:")
        const tbody = document.querySelectorAll('.drag-table .el-table__body-wrapper tbody tr')
        let _this = this
        for (let i = 0, len = tbody.length; i < len; i++) {
            Sortable.create(tbody[i], {
                filter: ".el-input",
                onEnd({newIndex, oldIndex}) {
                    if (newIndex > 7) {
                        console.log(newIndex, oldIndex)
                        return false
                    }
                    _this.resortTableData(i, newIndex, oldIndex)
                }
            })
        }
    },
```

# el-select
el-select拼音匹配 摘自：https://blog.csdn.net/li00828/article/details/85089358
1 npm install pinyin-match --save
2 :filter-method="pinyinMethod"
3 远程方法
```
 pinyinMethod(val) {
    const PinyinMatch = require('pinyin-match')
    if (val) {
        let result = []
        this.managernameDicts.forEach(
            i => {
                let m = PinyinMatch.match(i.code, val)
                if (m) {
                    result.push(i)
                }
            }
        )
        this.managernameDicts = result
    } else {
        this.managernameDicts = this.managernameDictsCopy
    }
}
```

## table
[ElementUI el-table 在flex下的宽度自适应问题](https://blog.csdn.net/qq_19694913/article/details/81144314)
这篇文章说到了一个重点：
>flex容器下的width:100%会一直向上继承，直到flex容器下第一级子元素，但是当某个子元素的宽度出现固定值并且大于flex伸展的宽度的时候，那么容器就不会收缩，自然也就触发不了resize事件了。
>
[element-ui的table组件在flex布局下的宽高自适应](https://blog.csdn.net/ohradiance/article/details/78980242)
>需要的效果：element-ui的table组件在垂直和水平方向能适应不同大小的显示区域，超出区域部分可实现滚动。进而强化对于控件自适应方面的理解。
看完这篇，要是能搞懂，会很开心吧，哈哈哈
目的：实现element-ui的table根据显示区域大小的自适应。
1，table要适配显示区域大小的变化，必须依赖滚动。(其实任何实际内容超出显示区域的情况都需要滚动)
2，table的横向纵向滚动都需要一个基本的前提条件--让table知道显示区域的大小。(这没啥好说的)
3，所以，我们可以用弹性布局，动态的改变table的显示区域大小。
4，如何让table准确知道当前显示区域的动态实时大小，就只有靠100%
>

悟道：经过以上两篇文章，加上自己的实践。一个不错的布局方式诞生了》》框架用position：relative；内部填充的部分，docker用absolute。
```
最近有些过于迷恋Flex，如果你只掌握一种布局，dangerous
#nav {
    background-color: #85d989;
    width: 100%;
    height: 50px;
}
#content {
    background-color: #cc85d9;
    width: 100%;
    position: absolute;
    top: 50px;
    bottom: 0px;
    left: 0px;
}
```

## Table行转列总结
[CSDN](https://blog.csdn.net/textalign/article/details/83863475)
1 组织Template
1.1 第一列：title
1.2 for dataList：取row中的ID作为colKey
```
for (int dataIndex = 0; dataIndex < dataList.size(); dataIndex++) {
    HashMap<String, Object> rowData = dataList.get(dataIndex);
    KeysCustomer keyNew = new KeysCustomer();
    keyNew.setKey(rowData.get(dateKsy).toString());
    keyNew.setName(rowData.get(dateKsy).toString());
    keyNew.setType(TkamcConstant.key_type_number);
    keyNew.setWidth("180");
    resultKeys.add(keyNew);
}
template.setKeysList(resultKeys);
```
2 组织TableData
2.1 for colKeys：遍历key
2.2 for dataList：对dataList的colKey赋值
```
List<Map<String, Object>> tableData = new ArrayList<>();
//组织tableData结构
for (int rowIndex = 0; rowIndex < keys.size(); rowIndex++) {
    KeysCustomer colKey = keys.get(rowIndex);
    Map<String, Object> row = new HashMap<>();
    row.put("TITLE", colKey.getName());

    for (int dataIndex = 0; dataIndex < dataList.size(); dataIndex++) {
        HashMap<String, Object> rowData = dataList.get(dataIndex);
        row.put(rowData.get(dateKsy).toString(), rowData.get(colKey.getKey()));
    }
    tableData.add(row);
}
```
x < dataList.size(); dataIndex++) {
    HashMap<String, Object> rowData = dataList.get(dataIndex);
    KeysCustomer keyNew = new KeysCustomer();
    keyNew.setKey(rowData.get(dateKsy).toString());
    keyNew.setName(rowData.get(dateKsy).toString());
    keyNew.setType(TkamcConstant.key_type_number);
    keyNew.setWidth("180");
    resultKeys.add(keyNew);
}
template.setKeysList(resultKeys);
```
2 组织TableData
2.1 for colKeys：遍历key
2.2 for dataList：对dataList的colKey赋值
```
List<Map<String, Object>> tableData = new ArrayList<>();
//组织tableData