# DC 调光

[逐渐远去的类DC调光 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/174293509)



> Oled 为什么需要pwm (em duty)是因为为了提升oled的良率，主要原理可以想成面板上非常多的用电压控制水量的水龙头(以三星的面板FHD 就有1080＊1920＊2个水龙头TFT)，水量大小就是电流大小，不同电流就是不同亮度
>
> 现在问题来了，理想上的水龙头控制电流都希望是非常准确，如果不准确会造成亮度不是我们预期的就会产生画面不均匀性，就是我们所谓的mura(绿屏门事件也是一种mura)，但是现在面板制程上都还是会有一些差异性，尤其在水量小的时候，所以在一定亮度以下水量就会比较难控制，但是手机一定还是得有均匀的低亮度画面啊，所以三星就想到一种方法，不要用很小的电压去调很小的水量，来得到很小的亮度，而是利用较大的电压来控制比较大水量，但是利用间隙打开跟关闭来控制总水量，因为人眼睛看到亮度是累积的，是总水量的概念，所以就出现了PWM，关闭时间越多亮度就越小(PWM占空比)，目前业界如果在active mode 都是4cycle,配合60Hz 帧率，就会有240hz ，目前oled 产品在一些亮度以下就会开启此功能
>
> ---小米手机部显示触控部副总经理 Calvin_吴仓志  [Oled 为什么需要... - @Calvin_吴仓志的微博 - 微博 (weibo.com)](https://www.weibo.com/6996948401/Hkk1j6sfO)



对于小米的硬件DC调光原理，在 AKR 社区上有所提及



> 小米的DC调光使用displayfeature向/sys/class/drm/card0-DSI-1/mipi_reg写入相关屏幕命令实现，具体算法在闭源的blobs里，想在类原生使用DC只能使用蛋丁DC或开发者拆官方DC轮子。



对于遮罩类 DC 调光，在 AKR 社区

[OP5/OP5T DC调光内核的问题修复 - AKR社区 (akr-developers.com)](https://www.akr-developers.com/d/160)

[DC调光进阶版的开发过程及思路 - AKR社区 (akr-developers.com)](https://www.akr-developers.com/d/273)

