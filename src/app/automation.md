---
icon: fa-solid fa-scroll
category:
  - 使用指南
tag:
  - 应用
  - 主界面
  - 规则
  - 行动
  - 变量
  - 自动化
---

# 自动化

::: info ClassIsland 欢迎您参与完善本条目☆Kira~

欢迎正在阅读这个条目的您协助编辑本条目。编辑前请阅读[条目编辑规范](../community/contributing.html)，并查找相关资料。ClassIsland 祝您在本文档度过愉快的时光。

:::

**自动化**是 ClassIsland 1.6 (Himeko) 的新增功能，旨在提供简单快捷的自动操作。

比如，您可以…

- 在视频展台开启时，自动将主界面移到屏幕右上角，并仅显示当前课程的倒计时；
- 在数学课前，自动打开白板；
- 放学后，自动关闭设备。

如果需要更高级的自动化功能，您还可以搭配专业自动化软件使用，如 [zTasker](https://everauto.net/cn/index.html)、[Power Automate](https://www.microsoft.com/zh-cn/power-platform/products/power-automate)

> [!warning]
> 自动化允许自动修改 ClassIsland 的各项设置，并调用外部程序，可能有一定安全风险。
> 不当的自动化编写可能对正常教学造成影响，请勿滥用。

> [!important]
> 自动化目前正在早期开发中，不建议用于生产环境。此功能在未来可能会产生较大的变动，并且**可能无法保证配置文件完全向下兼容**。欢迎在 [ClassIsland/ClassIsland#119](https://github.com/ClassIsland/ClassIsland/issues/119/) 讨论此功能。

## 概述

**自动化** (Automation)，曾称为**规则行动组**、**条件行动对**，即一对【规则集】与【行动】的组合。

![自动化设置界面](image\automation\自动化：应用设置界面.png)

**规则集** (Ruleset) 可以定义一些行为的触发条件。你也可以在主界面高级隐藏规则、组件隐藏规则等处见到它。

![规则集示例](image\automation\规则集示例.png)

**行动** (Action) 则可以定义一些操作，如更改应用设置、启动指定程序等。

![行动示例](image\automation\行动示例.png)

当规则集被满足时，其对应的行动会自动触发。您也可以添加【等待时长】行动来自定义执行的等待时间。

当规则集不再满足时，已经执行的行动会自动恢复。比如，已修改的应用设置将被自动改回。

![触发和恢复](image\automation\触发和恢复.png)

您也可以点击自动化设置页面右上角的【触发】和【恢复】来测试行动。

## 配置方案

和组件一样，您可以为自动化切换多个不同的配置文件，或者随时禁用所有或指定的自动化。

![](image\automation\自动化开关和配置方案.png)

您也可以来 [🙌展示台](https://github.com/ClassIsland/ClassIsland/discussions/categories/%E7%BB%84%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%88%86%E4%BA%AB) 与大家分享你的自动化方案。

## 技术性细节

1. 您可以拖动自动化进行排序，它们将会按照从上到下的顺序依次开始执行。

![拖动自动化以进行排序](image\automation\排序自动化.png)

2. 行动会创建一个 **设置叠层** (SettingsOverlay) 对应用设置进行临时更改，以便于多个行动的恢复。不过在临时更改期间，如果您手动修改了某个设置，那么该设置项将遵循手动的修改，不会再被恢复。

3. 设置叠层会遵循先来后到的顺序依次往上叠加。因此，如果您希望某一行动始终生效，需要对其他自动化的规则集设置排除以进行规避。

4. 在编辑完组件、自动化或档案后，请勿直接关机，这可能导致您的更改丢失。您需要手动关闭应用设置窗口（或手动退出 ClassIsland）以触发这些配置的保存。