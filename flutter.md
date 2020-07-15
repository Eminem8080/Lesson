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

