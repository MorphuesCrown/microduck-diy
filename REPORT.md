# 自己做一只 Microduck

核对日期：2026-10-25。资料来自 Pollen Robotics 公开仓库，以及社区复刻（fanhao375 / 机械行者Robo / jyg9）。这是第三方复刻路线，与 Pollen 无隶属关系。

官方整机标价 399 美元（税前、不含运费），预售从 2026-08-27 起，首批面向北美和欧洲，目标圣诞前发货。国内要自己做，走下面这条已经有人装出来并走过的路线。

## 先定这条

做 **飞特 HD-1910-C001 × 15 + Radxa Zero 3W + 官方 HAT D1 + 总线 IMU 小板**。

社区在这条路上已经装出整机，并用 2026-10-23 的复刻镜像做到站立和行走。打印工程、装配说明书、装配视频、中文 Studio 都在。飞特额定 4–8.4 V，和 2S 电池同一档。

Dynamixel XL330-M288-T 是官方舵机。官方 ONNX 策略按这套机构训练。XL330 额定 3.7–6.0 V，官方把它直接接在电池上，实跑约 6.6–8.2 V。个人买 15 颗，美国站大约 412 美元，欧洲含税可以到 600 欧元以上。要官方策略、并且接受超压和舵机花费，再走 XL330。两套舵盘配合件不能混打。

装配清单原表把舵机写成「飞特 HD1901M」。主仓和踩坑记录只认 **HD-1910-C001**。下单前对着卖家型号和舵盘照片核对，HL-2915 是 12 V 舵机，2S 电池带不动。

## 这只鸭子是什么

约 25 cm 高、14 cm 宽、800 g 以内的双足。15 个关节：14 个进强化学习策略，第 15 个是嘴。机载 50 Hz 控制环，主控是 Rockchip RK3566。官方软件（运行时、仿真、训练、ONNX 导出）是 Apache-2.0。Pollen 明确要求媒体不要把它说成开源硬件：可编辑整机 CAD、整机 BOM、装配文档、`imu_to_dxl` 原理图，官方都没有发。

社区能做，是因为 `microduck_rl` 里有仿真用的 MJCF 和 STL（CC BY-NC-SA），机械行者Robo 据此做成了可编辑 SolidWorks；HAT 板在 `elec_RPI_Robot_HAT` 里是完整生产文件。

## 开源边界

| 东西 | 状态 | 许可证 | 本地位置 |
|---|---|---|---|
| 运行时 `microduck` | 官方公开 | Apache-2.0 | `upstream/microduck` |
| 训练 `microduck_rl` 与 54 个仿真 STL | 官方公开 | 代码 Apache-2.0；网格 CC BY-NC-SA | `upstream/microduck_rl` |
| 官方策略 ONNX | Hugging Face | 随官方仓库 | `assets/policies` |
| RPI Robot HAT D1 | 官方公开，4 层、1.0 mm | Apache-2.0 | `upstream/elec_RPI_Robot_HAT/production` |
| KiCad 符号库 | 打开 HAT 工程才需要 | 随 `lib_KiCAD` | `upstream/lib_KiCAD` |
| 飞特 SolidWorks v2.2、XL330 v1.1 | 社区重建 | CC BY-NC-SA | `assets/cad` |
| 飞特 3MF、21 页装配 PDF、组件图 | 社区 | CC BY-NC-SA | `upstream/microduck-replica-cad` |
| `imu_to_dxl` / banana / dxl_hub 与固件 | 社区自绘 | Apache-2.0（community-kit） | `upstream/microduck-community-kit` |
| 飞特复刻镜像 20261023c | 社区 | 个人学习、非商用；模型不得随产品分发 | `assets/image` |

仿真 STL 用来对装配关系，打印以 CAD 仓库的 v2.2 工程为准。网格文件名 `np_f970` 和 `raspberry_pi_zero_2_w` 是上游占位名：电池买 **NP-F550**，主控买 **Radxa Zero 3W**。

## 钱大概花在哪

机械行者Robo 2026-10-23 装配清单原表合计 **2426.88 元**。舵机 15 × 95 = 1425 元，是大头。其余大约：

| 项 | 原表 | 动手时改这一处 |
|---|---:|---|
| 飞特舵机 ×15 | 1425 | 认 HD-1910-C001 |
| Radxa Zero 3W | 309 | 官方渠道无 eMMC 的 1G 或 2G，2026-09 快照大约 130 元。小店有卖到几百到一千多的 |
| 64 GB TF 卡 | 60 | 闪迪或三星，A1/A2。32 GB 也够，镜像说明推荐 32 GB、至少 8 GB |
| HAT | 120 | 可拼团，或用本地 Gerber 自己打 4 层板并 SMT |
| imu_to_dxl | 80 | 可拼团，或打 community-kit |
| 打印件 | 139 | 自己打就换成耗材。软下巴、软嘴、合体轮胎用 TPU |
| URT2 调试板 | 45 | 配 ID 用。口和飞特 2.0 mm 线对不上，要飞线 |
| NP-F550 | 行内总价 47 | 单价写 17、总价写 47，两数对不上。另买 NP-F 充电器，HAT 上没有充电电路 |
| IMX219 | 46.8 | 头部摄像头，安装转了 90°，软件里有补偿 |
| VL53L8CX | 49.5 | 8×8 ToF。固件也认 L5CX。L7CX 会被拒绝。L8CX 大板可能塞不进脸壳，优先小尺寸 L5CX |
| 轴承 22×16×4 ×11、15×10×3 ×3 | 约 47 | 另有 6×12×4 轮滑轴承 ×4，只做轮滑变体才需要 |
| 螺丝、螺纹胶、鞋底垫、banana 板 | 几十元 | M2 为主 |

原表 `SUM` 没把最后一行鞋底垫 16 元算进去。按官方渠道把主控从 309 调到约 130，整机仍在 **两千出头到两千五** 这个量级，到不了官方 399 美元的出厂价。HAT 若自己 SMT，4 层加贴片可能高于表上的 120 元。

## 一步一步

每一步做完再进下一步。舵机 ID 和零位在锁死螺丝之前做。

### 1. 只买一套配合件

飞特版用 `assets/cad/SolidWorks-FT2026-10-20.zip`（v2.2）和已经在仓库里的 `upstream/microduck-replica-cad/打印/microduck-飞特版-BambuStudio2026-10-20.3mf`。XL330 用 `SolidWorks-XL330-v1.1.zip`，该版没有现成整盘 3MF，要从零件导出 STL 再切片。

采购条目、数量、材料以 `upstream/microduck-replica-cad/BOM/README.md` 和同目录 Excel 为准。淘宝链接会过期，链接失效就按品名重搜。

### 2. 打印

Bambu Studio 打开 10-20 的 3MF。工程按 P2S、0.4 喷嘴、PLA Basic、层高 0.2 mm、5 盘排好。换打印机就重设参数。

- 结构件 PLA。
- 软下巴、软嘴顶部改 TPU。原表材料栏写 PLA，备注要求改软料。
- 合体轮胎是 TPU。这份 3MF 里仍是独立轮辋和轮胎；做轮滑变体时从 v2.1 源文件导出合体轮胎。走路件和轮滑件不要混装。
- 颈部、躯干底座、上腿加固板、轴承滚轮，清单建议能上铝合金就上。第一台用 PLA 也能装。

v2.2 相对旧版：头部上壳加了散热孔，左右上腿减小了间隙。

### 3. 打两块必要的板，再加两块小转接

**HAT，不要自己重画。** 生产文件：

`upstream/elec_RPI_Robot_HAT/production/PCB01186-D1_elec_RPI_Robot_HAT_PCB.zip`

同目录还有 D1 的 BOM CSV、贴片坐标 POS、原理图 PDF、装配 PDF、STEP。下单参数：4 层，板厚 1.0 mm，外形约 65.0 × 30.9 mm。BOM 约 123 颗，其中 EEPROM `U4` 等几行 DNP 不贴。有 VQFN codec 和 LGA IMU，手焊不现实，选 SMT。只打样不用打开 KiCad；要改原理图再把 `lib_KiCAD` 配上。

这块板没有充电，也没有 USB-C 供电入口。电池用外部 NP-F 充电器。Dynamixel 口是 JST EH 2.5 mm；飞特线是 2.0 mm，不能直接互插。

**imu_to_dxl。** 官方没有这块板的工程。用 `upstream/microduck-community-kit/hardware/imu_to_dxl`。它把 LSM6DSV16X 伪装成总线从机，ID 200，寄存器 124，控制环一次读 12 字节（陀螺 int16 ×3，四元数 fp16 的 xyz）。固件 1.6 是给 kissqy / 复刻镜像配套的 FT6 协议，和 1.5.x 不兼容，也不是在 1.5 上点一下升级。镜像 20261023c 会自动识别 FT6 和 DXL 2.0 的 124/12 布局。小板要事先刷好，镜像不会刷 MCU。

**banana_pcb 和 dxl_hub** 在同一套 community-kit 里：电池香蕉头取电，和躯干里的舵机分线。官方没有线束图，这是社区补上的走法。

### 4. 配舵机 ID，先不要装进壳

用 URT2。飞特调试板的 TTL 口比 AMP2.0 大，插不进，按踩坑记录飞线。飞特脚序是 `1=信号 2=Vcc 3=GND`。XL330 是 `1=GND 2=Vcc 3=信号`。空载配 ID 时 USB 5 V 够用，先用万用表确认端子上有 5 V。

波特率 1 Mbps。出厂可能显示 unknown，寄存器仍可写。每颗只留一只在总线上时写入：

| ID | 关节 | ID | 关节 |
|---:|---|---:|---|
| 20 | 左髋 yaw | 10 | 右髋 yaw |
| 21 | 左髋 roll | 11 | 右髋 roll |
| 22 | 左髋 pitch | 12 | 右髋 pitch |
| 23 | 左膝 | 13 | 右膝 |
| 24 | 左踝 | 14 | 右踝 |
| 30 | 颈 pitch | 32 | 头 yaw |
| 31 | 头 pitch | 33 | 头 roll |
| 34 | 嘴 | 200 | IMU 小板，不是舵机 |

来源是官方 `duck-ipc-proto` 的 `JOINT_IDS` / `JOINT_NAMES`。

### 5. 按组件装，锁紧前先归中

装配顺序：躯干 → 左腿（髋、髋 roll、大腿、小腿、踝脚）→ 颈和头 → 右腿。说明书是 `upstream/microduck-replica-cad/安装说明书/microduck装配安装说明书.pdf`（21 页）。视频是机械行者Robo 的 B 站合集《MicroDuck 从零安装教程》，一集一个部件：

1. [零件清单](https://www.bilibili.com/video/BV1RoHX68EFV/)
2. [小腿](https://www.bilibili.com/video/BV1Xppb6tECr/)
3. [大腿](https://www.bilibili.com/video/BV1ycpb6yEwB/)
4. [躯干](https://www.bilibili.com/video/BV1Kwpg6wE9G/)
5. [颈部](https://www.bilibili.com/video/BV1EEpg6nEkD/)
6. [头部](https://www.bilibili.com/video/BV1aKpE6hEzj/)

左右件分开，不要装反。螺丝对角预紧。每个活动关节装完就手转一圈，看干涉和夹线。关节件在通电归中之后再锁死。线从脖子过的是舵机总线和电源；主控、HAT、摄像头都在头里，MIPI 排线不穿过脖子。

### 6. 供电和 IMU 在第一次开机前接好

- 电池 NP-F550，2S。满电 8.4 V 顶着飞特电压上限，带载会掉到大约 6.6–8.2 V。
- HAT 给主板降压。整机发力时母线会塌，社区记录过整机重启。电源线要短、够粗，输入端可以并几百到两千微法的电容。第一次走路用电流够的电源或充满的电池，旁边留人。
- IMU 在第一次开机前接上。总线小板走 ID 200。若改用 I2C 模块，D1 HAT 头内那颗 LSM6DSV16X 占 0x6A，躯干模块设 0x6B，x 轴朝下、z 轴朝前。

### 7. 烧卡

镜像 `assets/image/microduck-replica-20261023c.img.xz`，712,068,864 字节。SHA256：

`10009c0a4aa963900719649836f5544036ad52cc15e3a0228eef05f6b747dab5`

核对：`shasum -a 256 -c microduck-replica-20261023c.img.xz.sha256`

用 balenaEtcher 或 Raspberry Pi Imager 的自定义镜像烧到空白卡。`.img.xz` 不用先解压。Windows 烧完若提示格式化，取消。

这份镜像只给 **Radxa Zero 3W + 飞特 HD-1910**。XL330 整机不要刷它。镜像免费，仅个人学习。里面的走路模型是作者个人非商业许可：不要卖烧好的卡，不要预装进收费的板子或整机。

### 8. 第一次开机

1. 插卡，舵机电源接上，上电。第一次大约 3 分钟：扩容、起名 `duck-` 加 4 位、认 IMU。
2. 手机连热点 `Microduck-xxxx`，密码 `microduck`。系统提示此网络无法上网时保持连接。
3. 浏览器打开 `http://10.42.0.1:8000/`。安卓打不开就先关移动数据。
4. 在页面里连家里的 Wi-Fi。鸭子会关掉热点，手机断开是正常的。之后用 `http://duck-xxxx:8000/`（Windows）或 `http://duck-xxxx.local:8000/`（苹果）。开了代理时 `.local` 可能 502，改用 IP，并把局域网设成直连。
5. 热点密码是公开的，Studio 默认没有登录密码。演示之前在「更多」里设密码。

完整原文：`upstream/microduck-replica/software/image/烧录和第一次使用.md`。

### 9. 按 Studio 上手清单做完再走路

1. 舵机零位：腿伸直、头摆正、嘴闭上，一键校准。
2. IMU 方向：托平，再按页面往前低头。更稳的是「站姿使能」后做站着校准，全程扶着。标定模式锁住姿态，不会自己平衡。
3. 写进主程序。写之前让鸭子坐下或卸力，舵机电源开着。写完主程序会重启，扶好。
4. 配蓝牙手柄，或先用网页摇杆。雷神 G50 Pro 拨到 Xbox 档。
5. 短按 Select 确认能马上卸力。按住 Select 约 2 秒会坐下、卸力并关机，测急停时不要按住。
6. 点站起来，再点开始走，轻推摇杆。周围留出空地。任何时候页面右上角「卸力」或空格键可以让它软下来。

手柄（Xbox 布局）：Start 站起后再按开始走或停下；左/右摇杆走和转；十字下坐下或站起；A 低头捡；X 前滚翻；LB/RB 左右踢；扳机张嘴。普通走路形态不要按住十字上 3 秒，那是切到轮滑。

飞特的位置计数方向和 XL330 相反，机械若照官方装法，15 颗会全体反向。零位和方向以 Studio 校准结果为准，不要只看仿真里的正负号。HD-1910 出厂 P/D 偏硬，走路发颤时先把 D 降下来再调，社区记录里用过 P3 / D0 这一档，代价是抬脚变低。

### 10. 确认传感器

摄像头是 IMX219，官方运行时默认旋转 90°。复刻镜像说明里，20261023c 的摄像头默认仍可能是测试画面，实拍要在 Studio 里再确认。ToF 地址常见 0x29。电池电压没有独立电量计，官方做法是读舵机上报的母线电压。

### 11. 想改动作，再训练

飞特机上的走路和起身模型已经在复刻镜像里，个人使用即可。官方 `assets/policies` 里的 ONNX（61 维观测、14 维动作、50 Hz）是给 XL330 机构的，不要直接灌进飞特鸭子。

要新动作：CUDA 机器上克隆完整的 `pollen-robotics/microduck_rl`（本地这份是稀疏检出，只有模型和网格），按 HD-1910 的力矩、间隙和方向重训，导出 ONNX。官方训练入口是 `uv run train Mjlab-Velocity-Flat-MicroDuck`。没有 NVIDIA GPU 时，社区有 Mac 上的 `jonathanhawkins/microduck-lab`，那是另一条训练栈。

XL330 且机械、总线、IMU 布局都与官方一致时，才用官方策略。安装形态是 `robotctl policy add`。

### 12. 走起来之后再加的东西

轮滑脚、踢球、捡东西都要在平地走路稳定之后再试。前滚翻和踢球周围留空间。官方还有 NFC、头内第二颗 IMU（HAT 上的 BMI088，运行时基本不用）、喇叭。这些不影响第一台站立。

## 官方软件栈，给 XL330 路线

主控同样是 Radxa Zero 3W。官方仓库是鸭子的脑子：`robotd` 跑 50 Hz 和舵机总线，`updaterd` 签名更新并可回滚，`configd` 管 Wi-Fi，`btd` 管手机蓝牙，`padd` 读手柄，`mediad` 走 WebRTC，`tofd` 读深度。总线是 `/dev/ttyS2`，1 Mbps，Dynamixel Protocol 2，单线半双工 TTL。

从空板到能跑，官方文档在 `upstream/microduck/docs/robot/`：`install-dev.md`、`install-by-hand.md`、`cheatsheet.md`。开发板流程会改设备树、关掉电机串口上的内核控制台，然后重启，这一次重启不能省。

## 还没有公开资料的地方

- 官方线束长度和走线卡扣。按实物留活动余量，用 community-kit 的 hub 分线。
- 电池触点。用 banana 板加 NP-F 弹片座，先在壳外量极性再焊。
- `imu_to_dxl` 的官方 MCU 型号。社区板是自己选的 MCU，协议对齐即可。
- 20261023c 对 DXL 2.0 IMU 的真板验收，发布说明里写的是尚未在你的鸭子上做完。刷卡后用 Studio 的识别结果确认，再做方向校准。
- 个人复刻的质量和间隙取决于打印和舵机零位，第一台预留返工螺丝和一根备用舵机线。

## 本地资产

根目录：`/home/megumi/Projects/microduck-diy`

| 路径 | 内容 |
|---|---|
| `upstream/microduck` | 官方运行时与设计文档 |
| `upstream/microduck_rl` | 仿真 MJCF 与 STL（稀疏检出） |
| `upstream/elec_RPI_Robot_HAT` | HAT KiCad 与 D1 生产文件 |
| `upstream/lib_KiCAD` | 打开 HAT 工程用的库 |
| `upstream/microduck-replica` | 复刻文档、踩坑、烧录说明、BOM |
| `upstream/microduck-replica-cad` | 3MF、装配 PDF、组件图、装配清单 |
| `upstream/microduck-diy` | 另一份中文装机笔记（wslengzhicheng） |
| `upstream/microduck-community-kit` | IMU / banana / hub 原理图与固件源码 |
| `assets/cad` | SolidWorks 发布包 |
| `assets/image` | 20261023c 镜像与校验 |
| `assets/policies` | 官方 ONNX 策略 |
| `assets/firmware` | community-kit 1.6 固件包 |

大文件若某次下载中断，在对应目录重跑 `gh release download`。固件源码要编译时，community-kit 需 `git clone --recurse-submodules`，当前检出可能没有 GD32 子模块。

## 许可

个人学习、自己装一台，可以用这些文件。网格、SolidWorks、装配图是 CC BY-NC-SA：署名、非商业、相同方式共享。复刻镜像里的动作模型不要放进收费产品。官方代码是 Apache-2.0，可以改，保留声明。
