# Microduck 自制笔记

自己做一只 Pollen Robotics Microduck 的步骤、采购口径和已核对过的文件。分步说明在 [REPORT.md](REPORT.md)。

推荐路线：飞特 HD-1910-C001 × 15、Radxa Zero 3W、官方 HAT D1、总线 IMU 小板，再用社区复刻镜像 20261023c 开机。官方 ONNX 策略是给 XL330 的，不要直接灌进飞特版。

## 仓库里有什么

- `REPORT.md`：从买件到走路的步骤
- `assets/policies/`：官方策略，61 维观测、14 维动作，清单写明 `servos: xl330`
- `assets/firmware/`：community-kit IMU 固件 1.6（FT6）
- `assets/cad/STEP-changed-parts-FT-2026-10-20.zip`：飞特 v2.2 改动件 STEP
- `assets/image/`：镜像的许可、校验和模型说明

两份 SolidWorks 和系统镜像超过 GitHub 单文件 100 MB，在 [Releases](../../releases) 里。

## 大文件校验

| 文件 | 字节数 | 校验 |
|---|---:|---|
| `SolidWorks-FT2026-10-20.zip` | 417656282 | 与 fanhao375/microduck-replica-cad v2.2 发布附件一致 |
| `SolidWorks-XL330-v1.1.zip` | 332776144 | 与同仓库 v1.1 发布附件一致 |
| `microduck-replica-20261023c.img.xz` | 712068864 | SHA256 `10009c0a4aa963900719649836f5544036ad52cc15e3a0228eef05f6b747dab5` |

镜像烧录前在同目录执行 `shasum -a 256 -c microduck-replica-20261023c.img.xz.sha256`。

## 上游

- https://github.com/pollen-robotics/microduck
- https://github.com/pollen-robotics/microduck_rl
- https://github.com/pollen-robotics/elec_RPI_Robot_HAT
- https://github.com/fanhao375/microduck-replica
- https://github.com/fanhao375/microduck-replica-cad
- https://github.com/jyg9/microduck-community-kit
- https://huggingface.co/pollen-robotics/microduck-policies

许可和署名见 [NOTICE.md](NOTICE.md)。
