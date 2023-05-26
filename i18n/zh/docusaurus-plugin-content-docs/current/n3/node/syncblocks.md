---
sidebar_label: '快速同步区块'
sidebar_position: 4
---

# 快速同步区块数据

Neo 客户端必须先完成与区块链的同步才能正常使用。由于区块链数据庞大，客户端同步时间通常很久，建议采用离线同步包加速同步过程。

## 第一步 - 获取离线包

1. 关闭客户端，进入[离线包下载页面](https://sync.ngd.network/)。

2. 在离线包下载页面，根据你所在网络点击 **N3主网** 或 **N3测试网** 标签，然后选择以下一种离线包进行下载 （无需解压）：

   - **全量离线包**：包含了最完整的区块高度数据，适用于初次运行的客户端。下载到的文件为 chain.0.acc.zip。
   - **增量离线包**：包含起始高度到结束高度范围内的数据，当你的客户端已经同步到增量包的起始高度之上时，可使用增量包继续进行同步。下载到的文件为 chain.x.acc.zip，x 为增量包的起始高度，如 chain.378997.acc.zip。

   ![](assets/sync_01.png)

## 第二步 - 放置离线包

:::caution
放置离线包时切勿修改离线包文件名，否则会导致无法同步。
:::

对于 Neo-CLI:

将下载的压缩包文件 chain.0.acc.zip 或 chain.xxx.acc.zip 直接放置到客户端 Neo-CLI 根目录下，如下图所示：

![](assets/sync_02.png)

对于 Neo-GUI:

将下载的压缩包文件 chain.0.acc.zip 或 chain.xxx.acc.zip 放置到客户端 Neo-GUI 根目录下的resources\build-neo-node 文件夹中，如下图所示：

![](assets/sync_05.png)

## 第三步 - 查看同步状态

再次打开客户端查看同步状态：

- 对于 Neo-CLI，输入 `open wallet <path>` 打开钱包后，输入 `show state` 查看区块同步状态，当画面显示连接数为 0 并且同步速度明显加快时， 说明已进入离线同步模式。当同步完成时会出现连接数。

![](assets/sync_03.png)

![](assets/sync_04.png)

- 对于 Neo-GUI，将发现客户端以超快速度进行同步。

![](assets/sync_06.png)

:::note
 - 进行离线包同步时，客户端无法与外界通信，此时 node 数为 0，且无法调用 API。当离线包使用完毕后，客户端会自动恢复与外界的通信。
:::
> - 也可以使用 Neo-CLI 的 `export blocks` 命令，将同步好的区块数据导出成离线同步包。 `export blocks` 后面无参数时默认导出所有区块数据，当附加 `<start> [count]` 参数时，可以从指定区块高度导出指定数量的区块数据，方便备份以及在原有区块数据上追加同步。相关信息请参见 [CLI命令参考](cli/cli.md) 。