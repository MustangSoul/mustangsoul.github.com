---
layout:     post
title:      "通用查询接口的结构化设计方式"
subtitle:   "工作总结."
date:       2015-09-22 17:00:00
author:     "Geekzhou"
header-img: "img/post-bg-01.jpg"
---

# 通用查询接口的结构化设计方式


## 处理流程
![处理流程](http://www.geekzhou.com/img/201509221751.png)
[链接测试](http://www.baidu.com)

##处理POST数据

1.处理时间参数
如果我们的查询语句是:

    SELECT * FROM `geekzhou` WHERE `op_time` >= '2015-09-22' AND `op_time` <= '2015-09-22' ORDER BY `op_time` DESC LIMIT

那么只能查到2015-09-22 00:00:00这一时刻插入的数据，因此如果传入的时间参数是Y-m-d格式的，需要对其进行初始化处理：

    $start_date = $this->request->POST['start_date']." 00:00:00";`
    $end_date = $this->request->POST['end_date']." 23:59:59";`

2.处理fields

凡是能够在外层处理的，尽量在外层处理


    if(!empty($fields)) {
        $fields = explode(',',$fields);
    }else {
        $fields = array('op_type','op_data','op_user','type','op_time');
    }


