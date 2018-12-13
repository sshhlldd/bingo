# bingo
宾果小游戏
# 接口说明
### 初始化与开数接口
```
Mock.mock('getdata', {//初始化与后续一次开数都获取此接口
                    data: {
                        numArr: [1, 2, 3, 4, 5, 6, 7, 8, 9, , 10, 11, 12, 13, 14, 15, 22, 24, 26, 30,
                            16, 17, 18, 19, 20 
                        ], //开数的数组 Array
                        isBegin: true, //游戏开始还是结束  boolean
                        maxNum: 30, //取数范围 int
                        "maxLine|1": [1, 2, 3], //连线的条数 int
                        logoImg: './images/logo.png' //logo 200*200 string
                    },
                    code: 0, //0代表成功 int 
                    msg: "成功", // string
       });
```
### 点击结束按钮回调函数
```
//返回数据参数说明
  data = {
                status: 成功或失败  string
                currLine: 5 //条数 int
   };
 resClick: function (data) { //点击结束后的回调函数  
                        console.log(data);
                        var html =
                            '<p style="font-size:16px;text-align:center;">確定退出遊戲嗎？</p>';
                        mypop("提示", html, function (obj) {
                            obj.attr("disabled", true);
                            $.ajax({
                                type: "post",
                                data: data,
                                url: 'getdata',
                                dataType: "json",
                                success: function (res) {
                                    obj.removeAttr("disabled");
                                    if (res.code == 0) {
                                       console.log("成功操作")
                                    } else {
                                        alert(res.msg);//错误
                                    }
                                }
                            });
                        });
                    }
```
