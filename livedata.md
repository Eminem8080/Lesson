1.LiveData 中bean对象必须为小写

2.databinding 中的 bindadapter注解 生效时机为：当网络请求或者数据变换是才会出发此注解的代码逻辑，注解不受承载物的生命周期控制

3.databinding+livedata+kotlin 中使用databingAdapter 一直编译失败，但是使用java就一切正常 在项目build中添加 apply plugin: 'kotlin-kapt' // 添加 kapt 插件支持
