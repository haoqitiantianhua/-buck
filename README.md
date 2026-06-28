# -buck
功能：可将12vDC公头锂电池的电压利用buck降压为9v 7v 5v三档输出，用两段ldo电路将12v转为3.3v输出
实物图
<img width="1920" height="1080" alt="实物图" src="https://github.com/user-attachments/assets/19ae27ae-e32f-4495-9ac5-3459231868f9" />


原理图
主电路
<img width="1476" height="393" alt="主电路" src="https://github.com/user-attachments/assets/a9c2fc51-af39-432a-846f-4146c4fa8aeb" />


电感选这么大的原因是最初设计最大电流为2A，2A的纹波电流在0.4A-0.8A之间，我觉得又不是量产也不怎么需要考虑成本，冗余还是留大一些比较好，纹波电流就按0.8A算的，后来觉得我没有用得到2A大电流的使用场景以及懒得做过流保护，最终直接在输出端接了个1A的保险丝，现在电路最大输出电流为1A，由于电感已经到货了也就没去更换大小，目前来看用33uh的电感也没对我的电路造成什么影响
mos驱动电路
<img width="552" height="417" alt="驱动电路" src="https://github.com/user-attachments/assets/25d67e9a-27cd-4797-abdf-74929bbbbaa8" />


供电电路与ldo3.3v输出
<img width="828" height="684" alt="ldo输出与供电电路" src="https://github.com/user-attachments/assets/3e3aef3b-ad08-4571-8a94-0b6897bea631" />


注：12v转5vldo原理图的输入端贴片电容耐压为10v，实际输入为12v，记得更换合适耐压的贴片电容
单片机与屏幕
<img width="696" height="582" alt="单片机与屏幕" src="https://github.com/user-attachments/assets/278795ab-97ea-451f-931d-247e9c004c4f" />


由于最开始设计的时候没意识到串口调试的重要性，导致我手里的板子是没有串口调试针的，最终只好开动脑筋焊了两根杜邦线上去当调试针（
PCB
<img width="1772" height="881" alt="pcb" src="https://github.com/user-attachments/assets/4b9998bb-9d8e-4a8c-9468-5a508d5bfccf" />


调试针旁边的丝印是对应串口调试器的，不是对应单片机的
使用说明
DC头旁边的自锁按钮为电路总开关，单片机旁的按钮从左到右依次对应9v 7v 5v，单片机供电由ldo输出5v到单片机5v供电引脚，因此烧录调试时不需要烧录器与调试器供电，防止烧坏芯片
调试思路
先确保LDO电路跑通，再确保buck电路
buck电路：先pwm跑通确保电路正常→再调试串口，确保串口能发送信息→调试adc，确保adc正常→oled电路正常（未实现）


测试结果
5v空载
<img width="810" height="1440" alt="5v空载" src="https://github.com/user-attachments/assets/0bf67fe8-39e0-4a79-9ff4-bb674bc6e769" />
<img width="1920" height="1080" alt="5v电压" src="https://github.com/user-attachments/assets/bf434c05-652b-4d52-a66c-742a276ed506" />


7v空载
<img width="1080" height="1920" alt="7v电压（空载）" src="https://github.com/user-attachments/assets/f4d61bc1-2294-471d-9b03-b71be830e138" />
<img width="1920" height="1080" alt="7v电压" src="https://github.com/user-attachments/assets/b419c958-71fc-4a42-8ea1-82f99c611708" />


9v空载
<img width="810" height="1440" alt="9v空载" src="https://github.com/user-attachments/assets/c64c2429-5871-492f-8ec6-c6df10435754" />
<img width="1920" height="1080" alt="9v电压" src="https://github.com/user-attachments/assets/2d3f1dc5-bda3-4f9f-bee4-b8fce6e77df2" />
轻载测试（220欧电阻）
开环电路带载由于负载分压导致不可避免的电压减小，这个由于我现在还不会pid暂时没法解决，等以后有机会会补上闭环控制的


5v
<img width="810" height="1440" alt="5v带载 " src="https://github.com/user-attachments/assets/7fb38331-62da-4b36-8164-f87e0220c717" />
7v
<img width="810" height="1440" alt="7v带载" src="https://github.com/user-attachments/assets/1f559fd0-7144-480c-855f-7f0df4113509" />


9v
<img width="1080" height="1920" alt="9v带载" src="https://github.com/user-attachments/assets/8a4c4e0a-1116-4e8d-86f0-9697a9c8680b" />


纹波测试（空载）
纹波大小一般在20mv-40mv之间跳动，而且我的示波器接地有点问题导致结果可能有点市电的干扰，所以纹波具体大小我也不太确定


5v纹波
<img width="1440" height="810" alt="5v纹波" src="https://github.com/user-attachments/assets/0ecdd26d-0778-4795-b92e-f0ac8ffee899" />


7v纹波
<img width="1440" height="810" alt="7v纹波" src="https://github.com/user-attachments/assets/5940562c-fbba-47c3-a6ab-cbd3fbb94f17" />


9v纹波
<img width="1440" height="810" alt="9v纹波" src="https://github.com/user-attachments/assets/7da072e3-0a31-4a1b-9ca3-747b3b7404ac" />




