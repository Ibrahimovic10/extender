main.go文件： 首先会执行init函数，设置随机数种子。然后执行main函数来设置路由，为“htttp://localhost:8888”路由的GET()及POST()方法注册handler。最后`http.ListenAndServe(":8888", router)`将这个router绑定到本机的8888端口。  
  
router.go文件： 包含main.go中所需的三个handler。主要是处理请求，以及调用过滤和打分函数  
  
priorities.go文件： 实现了打分函数，打分方法为生成0到schedulerapi.MaxPriority之间的随机数（包括两端），该随机数就是分数。  
  
pridicates.go文件： filter函数调用podFitsOnNode函数判断某个pod是否适合某个node，并将搭配成功的放在一个数组里，将搭配失败的放在另一个数组里，最后作为结果返回。podFitsOnNode函数调用LuckyPredicate函数来判断pod是否合适node。而LuckyPredicate函数判断是否合适的方法就是获取一个整型随机数0或1，判断是否属于偶数，若是偶数则合适，否则不合适。