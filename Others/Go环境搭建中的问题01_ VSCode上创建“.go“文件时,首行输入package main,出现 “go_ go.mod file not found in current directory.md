@[toc]

# 1. 背景

1. go版本: 1.19.2 windows/amd64

2. VSCode

# 2. 问题描述

* 当第一次安装golang且配置好全局变量(注意: 因为这里想使用go的模块功能管理包,所以在环境变量中就没修改GOPATH,GOPATH还是安装Golang时,系统默认配的路径, 打开VSCcode, 如下所示的目录结构, 在test.go首行输入"package main"(main是包名),出现如`Figure 1`的错误

  ![image-20221021230729777](https://img-blog.csdnimg.cn/img_convert/5690094557ccdb8cbd2545c6465f0b49.png)

​                                                                                                   **<u>Figure 1</u>**                                



# 3. 问题解决: 三种办法

## 1. 第一种: 在终端下, 输入`go mod init main`生成go.mod文件(推荐)

* 在你所写的go文件的同一目录或者GOPATH/src下,在VS新建一个终端,在终端下输入`go mod init main`. 具体操作如`Figure 2`

  ![image-20221021004058255](https://img-blog.csdnimg.cn/img_convert/8852d26a42e9bd7cb7b0d97c542b0fee.png)

  ​															                              		**<u>Figure 2</u>**  

## 2. 第二种: 将`GO111NODULE`设置为`off`

* 在`Windows PowerShell`下, 输入`go env -w GO111MODULE=off`(==必须要带有"-w"==),也就是不起用模块管理包,具体如`Figure 3`.

  ![image-20221021004301624](https://img-blog.csdnimg.cn/img_convert/885688a4b837637e24ee07d2d522f84d.png)

  ​                                                                                                   **<u>Figure 3</u>**  

## 3. 第三种: 删除go插件

* 直接删除或者禁用go插件.  然后点击右上角的三角标(安装Code Runner后出现,图), 就可以正常运行了

  ![image-20221021004533762](https://img-blog.csdnimg.cn/img_convert/46da09fae36833fe4d4606d68f17645a.png)



​																		                    		**<u>Figure 4</u>**  

# 4. 问题原因

* ①在VSCode上安装了go插件(Figure 5), ②GO111MODULE"被设置成了"on"(可以在PowerShell,输入go env查看. Figure 6),  且③在go文件下, 没有所在的目录下, 没有生成go.mod文件(Figure 7). 其中①是出错的源头, 这些错误都是go插件检查出来的(我的VS的右下角也报了一堆错误).

  ![image-20221021003607891](https://img-blog.csdnimg.cn/img_convert/e930a635c69b29f626259fdfd2aa9473.png)

  ​												                                               **<u>Figure 5</u>**  				

  ![image-20221021003801246](https://img-blog.csdnimg.cn/img_convert/4ca7c388d2614cb32002ba0901584ed9.png)

  ​																						            	**<u>Figure 6</u>**  

  ![image-20221021003846606](https://img-blog.csdnimg.cn/img_convert/36512ab225e8101d5024260c86b61388.png)

  ​																					                     **<u>Figure 7</u>**  

# 5. Summary

* 在“GO111MODUDLE=on” 时, 表示要生成go.mod文件, 来管理包,当go插件检测出没有go.mod文件时,就会报相应的错, 最好的办法就是生成go.mod文件.

# 6. References

1. [go mod使用](https://www.jianshu.com/p/760c97ff644c)
