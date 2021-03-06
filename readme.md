**baseModule.js说明**
===================

**baseController**
-------------

> **参数说明**

> - 1 对于jquery对象扩展了两个方法warn和succes，一个弹出框方法，基于非常漂亮的弹出框组件swal.js
> - 2 对于以下方法会触发isUILock=true,可绑定该属性监听页面是否有任何xhr请求：
         lockButton selectedFileChange(如果选择立即上传模式) pageLoading requesting
> - 3 对于以下方法会触发isUILock=false,可绑定该属性监听页面是否有任何xhr请求：
pageLoaded requestEnd unlockButton formDataUpdateSuccess uploadSuccess uploadError selectedFileSizeInvalid imgSizeInvalid




**laydate**(日历指令)
-------------
！！确保laydate.js引入才能正常工作
**demo**
```
<laydate style="width:50%;float:left;" ngmodel="ms.selectedDate" class="form-control"></laydate>


如果样式不正常引入一下即可：
.laydate_body .laydate_y .laydate_yms{
        width:122px;!important;
    }
    .laydate_body .laydate_bottom{
        height:30px;!important;
        padding-top:10px;!important;
    }
    .laydate_body .laydate_ym .laydate_yms{
            top:23px;!important;
    }
    .laydate_body .laydate_top{
        background-color:transparent;!important;
    }
    .laydate_body .laydate_table thead th{
        border:none;!important;
    }
    .laydate_body .laydate_y{
        width:122px;!important;
    }
    .laydate_body .laydate_top{
        height:30px;!important;
        border: 1px solid #ccc;!important;
        border-bottom: none;!important;
    }
    .laydate_body .laydate_table{
        height:160px;!important;
    }
```


**jqueryUiMultiSelect**(基于jquery-ui和jquery.multiselect.js插件的下拉多选指令)
-------------

**demo**

```
<jquery-ui-multi-select width="50%" options="multiSelectOptions" selected-change-fn="onMultiSelectChange"></jquery-ui-multi-select>


$scope.multiSelectOptions=[
                {
                    labels:'全部选项',
                    //items:'联系人 联系电话 孩子姓名 孩子性别 孩子年龄 住址'.split(' '),
                    items:[
                        {
                            value:'联系人'
                            //,selected:true
                        },
                        {
                            value:'联系电话'
                        },
                        {
                            value:'孩子姓名'
                        },
                        {
                            value:'孩子性别'
                        },
                        {
                            value:'孩子年龄'
                        },
                        {
                            value:'住址'
                        }
                    ]
                }
            ]

            $scope.onMultiSelectChange=function(values){
                var values_arr=values.split(',');
                var arr=[];
                var map={
                    '联系人':'name',
                    '联系电话':'phoneNum',
                    '孩子姓名':'childName',
                    '孩子性别':'childSex',
                    '孩子年龄':'childAge',
                    '住址':'address'
                }
                for(var i in values_arr){
                    arr[i]={

                        key:map[values_arr[i]],
                        value:values_arr[i]
                    }
                }

                //var fields={
                //    fields:arr
                //}
                ms.formData.SHI_WU.fields=arr;
                console.log('this is the values arr------:',arr);
                //console.log("multi select changed");
            }
```
指定一个方法当元素激活时候空格键被按下执行的动作




**noneSelectMsg**(为select没有东西选中的时候增加一个提示信息:默认是请选择)
-------------
**demo**

```
<select ng-model='' ng-options='' noneSelectMsg='请选择一个项目'></select>
```


**debuger**(调试指令)
-------------
指定ngobj让该对象显示在页面上以观察变化


**responseSpaceAction**(响应空格键)
-------------
指定一个方法当元素激活时候空格键被按下执行的动作

**responseEnterAction**(响应回车键)
-------------
指定一个方法当元素激活时候回车键被按下执行的动作

**responseEscAction**(响应esc键)
-------------
指定一个方法当元素激活时候esc键被按下执行的动作

**pagination**(分页指令)
-------------

**demo**
```
<pagination
res-total-num-key="total"
page-handler-num="10"
page-size="10"
url="/test/fetchData?page={currentPage}&pageSize={pageSize}"
datamodel="obj.data"
transform-res-data-fn="transformResData">

</pagination>


<li ng-repeat="item in obj.data">
            {{item.id}}<br>{{item.name}}
        </li>



$scope.transformResData=function(data){

                    }
```


> **参数说明**

> - **res-data-key**  数据获取成功后服务器返回的数据中代表数据集合的key
> - **page-handler-num**  分页控件中控制页面跳转的元素的数量(以下简称handler)
> - **url**  获取数据的url
> - **datamodel**  绑定的数据模型
> - **transform-res-data-fn**  用于对获取到的数据进行处理，接收一个参数服务器返回的数据集合，通常为数组类型，要求返回对数据集合加工之后的数据集合
> - **init-page**  默认获取该参数指定的页数的数据，不传的话默认为1
> - **res-total-num-key**  数据获取成功后服务器返回的数据中代表数据总记录数的key
> - **page-size**  声明每页存在的数据条目数量


> **补充说明**
>
> - 指令独立作用域内置属性可用{name}的属性访问到，比如demo中url的值为"/test/fetchData?page={currentPage}&pageSize={pageSize}" ，其中**currentPage**表示当前页数（从第1页到最后一页，不存在第0页），**pageSize**表示每页数据条目数量

> **事件说明**
>
> - **paginationDataLoaded**  数据获取成功触发，p1-服务器 返回的信息，p2-$scope,p3-options,p4-$element
> - **paginationDatafetching**  开始获取数据时触发，p1-$scope,p2-options,p3-$element


**upload**(文件上传指令)
-------------

**demo**
```
<upload
srckey="{{CONFIG.UPLOADER.SRC_KEY}}"
srcmodel="ms.formData.SHI_WU.src"
btntext="奖品图片"
multi="{{CONFIG.UPLOADER.MULTI}}"
url="{{CONFIG.UPLOADER.URL}}"
ext="{{CONFIG.UPLOADER.EXT}}"
type="{{CONFIG.UPLOADER.TYPE}}"
maxsize="{{CONFIG.UPLOADER.MAX_SIZE}}"
width="{{CONFIG.UPLOADER.WIDTH}}"
height="{{CONFIG.UPLOADER.HEIGHT}}"
auto="{{CONFIG.UPLOADER.AUTO}}">
            <img ng-src="{{ms.formData.SHI_WU.src}}">
        </upload>
```

> **参数说明**

> - **multi**  1表示启用多文件上传，0表示只允许单文件上传
> - **url**  文件上传的server端地址
> - **type**  文件类型：img或者image表示图片，excel表示excel，*表示任意类型
> - **ext**  扩展名规则配置，逗号分隔
> - **maxsize**  用允许的最大文件体积大小
> - **width**  图片文件的宽度，数字表示特定，*表示无限制
> - **height**  图片文件的高度，数字表示特定，*表示无限制
> - **auto**  是否启用自动上传
> - **responseDataReader**  在绑定返回的数据前对数据进行处理的函数，参数表示处理前的数据
> - **key**  向server端发送数据时候单文件formData中append时候使用的字段名称
> - **srcmodel**  返回的数据指向的数据模型，不仅仅限于图片上传的返回信息，理论上任意类型皆可
> - **srckey**  从返回的数据中根据srckey定义的namespace字段名查找对应的数据
> - **btntext**  上传图片按钮的文字说明







> **事件说明**
>
> - **selectedFileExtInvalid**  选取文件扩展名不合法时触发，p1-错误信息，p2-$scope,p3-options,p4-$element
> - **selectedFileSizeInvalid**  选取文件大小不合法时触发，p1-错误信息，p2-$scope,p3-options,p4-$element
> - **imgSizeInvalid**  图片文件宽高不合法时触发，p1-错误信息，p2-$scope,p3-options,p4-$element
> - **uploadstart**  文件开始上传时时触发，p1-$scope,p2-options,p3-$element
> - **uploading**  图片上传过程中触发，p1-$scope,p2-options,p3-$element
> - **uploadError**  文件开始错误时触发，p1-错误信息，p2-$scope,p3-options,p4-$element
> - **uploadSuccess**  文件上传成功时触发，p1-服务器返回的信息，p2-$scope,p3-options,p4-$element









**selectAllCheckbox**(复选框全选指令)
-------------

**demo**
```
<select-all-checkbox item-flag="isSelected" checkboxes="ListOfItems" is-all-selected="AllSelectedItems" is-none-selected="NoSelectedItems"></select-all-checkbox>select all
         <div ng-repeat="item in ListOfItems">
         <input type="checkbox" ng-model="item.isSelected" />{{item.desc}}

         $scope.ListOfItems = [
         isSelected: true,
         desc: "Donkey"
         }, {
         isSelected: false,
         desc: "Horse"
         }];


         </div>
```


> **参数说明**

> - **checkboxes**  复选框使用的数据模型
> - **is-all-selected**  初始状态下是否全部选中
> - **is-none-selected**  初始状态下是否全部未选中
> - **item-flag**  每一个复选框对应的数据模型里表示是否选中的属性（boolean类型）



**baseService**(base这个module下的一个service，大多为公共方法)
-------------


> **方法说明**
>>**需要angular支持的方法：**


> - **multiHttp**  并发执行多个http请求，p1-请求url集合数组，p2-cb，参数为p1依次对应请求返回信息
> - **locker**  一个ui-lock工具，参数为dom节点jquery实例，返回一对象，包含：
> isLocked  表示该元素 是否处于上锁状态
> lock  锁住该元素，同时触发$rootScope的lockButton事件，参数为该元素
> unlock  解锁该元素，同时触发$rootScope的unlockButton事件，参数为该元素



>>**可独立使用的方法：**



> - **tpl**  微型模板匹配
> - **getFormDataByMap**  通过一个mapping的字面量对象查找对应的数据并生成集合对象，p1-formData,p2-map对象
> - **reverseMap**  翻转map对象,p1位map对象
> - **toggleArrayElement**  检查元素是否在数组中，存在则删除，不存在则push进去，p1-元素，p2-数组
> - **isRepeat**  检测数组中是否存在重复元素，p1-数组
> - **bubbleSort**  冒泡排序(升序)，p1-数组
> - **parseUrl**  将页面url转换成map对象，p1-链接，不存在则默认解析location.host
> - **getDataByModel**  通过modelstr从对象中获取数据,p1-数据集合对象，p2-modelstr,p3-读取失败返回的值，默认为null
> - **bubbleSort**  冒泡排序(升序)，p1-数组
> - **setDataByModel**  通过modelstr设置对象的属性
> - **getTargetScopeByModel**  通过modelstr依据当前$scope获取目标父$scope，p1-当前$scope，p2-modelstr
> - **isDate**  检查p1是否是类似于yyyy-mm-dd的日期形式
> - **filter**  通过p2这个数组中定义的字段名称从p1这个formData中过滤掉
> - **isDateTime**  检查p1声明的字符串是否是p2这个datetime类型，支持'y-m-d h:i:s'和'y/m/d h:i:s'
> - **getMapByObjIndex**  通过p1(下标从0开始)这个index从p2这个obj中取的一个map，格式为{k:"",v:""}


> - **isSequentFromNo1**  通过p1这个数组从第一个元素开始是否是从1开始的连续的数字
> - **isNull**  如果p1这个变量是空字符串或者是null或者是undefined就返回true
> - **isExist**  如果从p1这个对象中无法读取到p2这个属性引用或者读取失败就返回false，否则返回true
> - **getArrayByRepeatElement**  将p1这个对象复制p2次，然后返回一个新的数组，包含的每一项是p1这个对象
> - **getDateStr**  获取y-m-d格式的日期，p1表示从今天起相加的天数，-1表示昨天...，默认为0(今天)
> - **debounce**  节流函数:function(func, wait, immediate)

>/*
         节流函数
         // Usage
         var myEfficientFn = debounce(function() {
         // All the taxing stuff you do
         }, 250);
         window.addEventListener('resize', myEfficientFn);
         */
> - **poll**  期望状态检查:function(fn, callback, errback, timeout, interval)
> /*
         期望状态检查
         // Usage:  ensure element is visible
         poll(
         function() {
         return document.getElementById('lightbox').offsetWidth > 0;
         },
         function() {
         // Done, success callback
         },
         function() {
         // Error, failure callback
         }
         );
         */
> - **once**  function(fn, context)
> /*
         once函数
         // Usage
         var canOnlyFireOnce = once(function() {
         console.log('Fired!');
         });
          canOnlyFireOnce(); // "Fired!"
         canOnlyFireOnce(); // undefined
         */
> - **getAbsoluteUrl**  getAbsoluteUrl(url)获取url链接的绝对路径
>getAbsoluteUrl:(function() {
            var a;
            return function(url) {
                if(!a) a = document.createElement('a');
                a.href = url;
                return a.href;
            };
        })(),
> - **sheet**  插入样式表
/*
         插入样式:
         // Usage
         sheet.insertRule("header { float: left; opacity: 0.8; }", 1);
         */
