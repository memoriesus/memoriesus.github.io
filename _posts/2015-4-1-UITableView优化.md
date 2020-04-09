---
post: page
title: UITableView优化
tags: [iOS,UITableView]
comment: true 
---
## UITableView优化
* 复用cell
* 缓存cell
* 缓存高度
* 减少subview的数量，使用drawRect绘制，这样可以用GPU离屏渲染
* 避免图形特效，图片缩放颜色渐变等
* 设置不透明
* 不要阻塞主线程，将处理放到子线程中去处理设置最大线程数为2，利用NSOperationQueue的maxConcurrentOperationCount为2
