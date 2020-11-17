# Mini T12焊台-基于Arduino平台-Atmege328p-au
![](https://github.com/jie326513988/mini-T12/blob/main/Picture/1.jpg)
### 2020-11-15 V1.01程序更新 1.降低PWM频率为15HZ，手柄和mos的声音几乎没有了！之前为61HZ，声音还是有一点的。2.调节PID运行间隔。（31862字节，ide 1.8.13）
### PCBV1.7发现三处设计缺陷，完成以下步骤可正常使用。新的PCB V1.8，长度短5.3mm，DC插头伸出PCB板1.5mm。
* 请移除26V的TVS管
* 请移除靠近单片机的10uh电感，改成直连
* 10Ω电阻（R3）改为4.7KΩ，4.7KΩ电阻（R4）改为10KΩ
#### 默认支持深圳头，更换其他厂商的头需要自行校准温度曲线
#### 一定要使用我提供的U8g2库，否者无法显示中文和提示内存过大无法编译
#### 缺点就是PID温控超调回正时间过长，有能力的小伙伴可自己调节pid参数。
#### 本人喜欢温度显示真实一点，故采用显示平均温度的方案（8次温度采样的平均值）。
#### 当设定温度和平均温度的差值<=3度时就显示平均温度，所以看着会上下浮动1-2度是正常的。
* 可以在菜单设置里旋转屏幕显示的方向，方便不同的人群
* 动态调参PID
* 稳定时显示5次采集到的平均温度，其他时候显示实时温度大概500ma刷新一次
* 取消电流传感器，主界面取消电流显示改为显示PWM百分比
* 使用4段温度拟合温度曲线，4项式公式计时，可在设置菜单“校准”选项调整
* 休眠计时和息屏倒计时改用定时器2计时
* 息屏显示，无加热无操作3分钟后进入，息屏时显示环境温度，随机平滑移动
* 开机提示音和平滑过渡的开机界面
* 休眠时自动保存当前设置温度到eeprom
* 待机功耗8.8ma 息屏待机功耗6.4ma
#### 观看视频 https://www.bilibili.com/video/BV1vf4y1B7Xa
#### 按键功能定义
* 长按操作（5下短音最后1下长音）
  * 主界面，进入设置界面
  * 其他界面，退出至主界面
* 双击操作（2下短音）
  * 主界面，加热或停止状态切换
  * 其他界面，无
* 单击（1下短音）
  * 主界面，无
  * 设置界面，进入二级菜单
  * 二级菜单，切换数值更改选中状态，或确认更改数值，无选框状态则退出至一级菜单
#### 菜单选项
* PID
  * P
  * I
  * D
* 休眠
  * 休眠时间
  * 休眠温度
* 屏幕
  * 屏幕亮度
  * 屏幕方向
  * 编码器方向
* 电源
  * 基准电压
  * 电源电压
  * 低压报警
* 校准
  * 调节曲线第1段温度
  * 调节曲线第2段温度
  * 调节曲线第3段温度
  * 调节曲线第4段温度
  * 运行曲线拟合程序校准温度曲线
* 烙铁
  * 冷端补偿
  * 开机加热
  * 重置
#### 校准温度曲线的方法
* 1.准备好能测量0-500摄氏度的设备，探头建议使用裸装，以免外壳热传导导致热量损失测量不准
* 2.将探头紧压住烙铁头发热前段（上锡部分再下来一点），一定要紧紧压住，不然也会测量不准
* 3.放置好烙铁头以免校准时烫伤手或物品！
* 4.接上电源，从控制板进入‘校准’界面，将空心选框移动至第1段温度处（即对应的ADC 10下面）
* 5.按下确认键，此时空心选框变成实心选框，烙铁头开始加热，等待最下方的‘Now ADC’值稳定在一定的范围，与第一行相应的ADC值差不多即可（此时是ADC 10）
* 6.使用测量设备测量烙铁头的温度，将第1段温度调至测量得到的温度（实心选框状态可旋转旋钮调节数值）
* 7.依次测量剩下的第2段、第3段、第4段温度并输入至控制器
* 8.测量完4段温度后将光标移至Save，按下确认键，等待程序计时温度曲线
* 9.计算完会显示P系数界面，，再按下确认键即可退出校准界面
* 10.在主界面准备进行二次校准
* 11.在主界面开启加热至第二段校准的温度，如265，则加热至260度，若显示温度比实际高的话就到校准界面调高第二段温度，低则调低
* 12.依次加热至第三第四段温度并校准，直至自己满意为止
* 13.进入到“烙铁”选项，将冷端补偿温度改为此时主界面所显示的环境温度值（屏幕右上角），完毕。

![](https://github.com/jie326513988/mini-T12/blob/main/Picture/2.jpg)
![](https://github.com/jie326513988/mini-T12/blob/main/Picture/7.jpg)
![](https://github.com/jie326513988/mini-T12/blob/main/Picture/3.jpg)
![](https://github.com/jie326513988/mini-T12/blob/main/Picture/4.jpg)
![](https://github.com/jie326513988/mini-T12/blob/main/Picture/5.jpg)
![](https://github.com/jie326513988/mini-T12/blob/main/Picture/6.jpg)
