### 1.水平列表

水平列表教程 https://flutterchina.club/cookbook/lists/horizontal-list/

例子中使用的child为container,当我使用listTile时,包含有leading 就会报错:

```
Leading widget consumes entire tile width. Please use a sized widget.
'package:flutter/src/material/list_tile.dart':
Failed assertion: line 1353 pos 7: 'tileWidth != leadingSize.width'
```

原因：

```
leading: new Icon(Icons.ac_unit,size: 50,) //获取不到宽高规格
leading: new Image.asset('assets/imgs/bg.png',) //修改为普通image
```

并且外层容器必须显示的指名宽度 ,否则会报错：

```
I/flutter (31839): The following assertion was thrown during performLayout():
I/flutter (31839): BoxConstraints forces an infinite width.
```



#### 2.ListView没有和AppBar一起使用时，顶部空白

**ListView头部有一段空白区域，是因为当ListView没有和AppBar一起使用时，头部会有一个padding，为了去掉padding，可以使用MediaQuery.removePadding:**

```dart
Widget _rubbishList(){
    return MediaQuery.removePadding(
        removeTop: true,
        context:  context,
        child: Container(
            margin: EdgeInsets.only(left: 20,right: 20),
            height: ScreenUtil().setHeight(700),
            child: ListView.builder(
                itemCount: rubbishList.length,
                itemBuilder: (context,index){
                  return _cardItem(index);
                }
            )
        )
    );

  }
```



#### 3.[flutter中如何监听键盘弹出关闭](https://segmentfault.com/a/1190000022495736)

#### WidgetsBindingObserver & didChangeMetrics

这个组件可以监听页面的一些生命周期，并且其中有一个回调didChangeMetrics可以监听界面高度的变化。其中键盘的弹出和收起这些其实都属于高度的变化自然也是可以监听到的。