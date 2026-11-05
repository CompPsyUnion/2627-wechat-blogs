# 电脑只有一个 C 盘？带你认识磁盘分区

当你打开“此电脑”时，有没有发现里面只有一个 C 盘？照片、作业、游戏和软件都放在一起，用久了就像在一个大柜子里找东西。要是能再分出一个盘来放文件，会不会顺手一点？

我们这次就用 Windows 11 来聊聊磁盘分区，再一起看看怎么从现有空间里分出一个新盘。

## 一个大柜子，分成几个抽屉

让我们把硬盘想成一个柜子，分区就像在柜子里隔出几个抽屉。C 盘、D 盘可以是同一块硬盘上的不同区域，你可以按自己的习惯整理文件，就好像不同的抽屉放不同的东西一样。

![一块硬盘分成两个区域的示意图](img/disk-partitions.png)

这里有一点要注意：**分区不会凭空增加硬盘容量**。如果 C 盘和 D 盘来自同一块硬盘，硬盘损坏时两个区域都可能受影响。因此，D 盘不是备份：重要文件还要另存到外置硬盘或其他独立位置。

## 动手之前，先准备一下

1. **先备份重要文件。** 作业、照片这些珍贵的东西，可以先复制到外置硬盘或其他独立位置，再打开几份副本，确认能正常读取。
2. **看看空间够不够。** 新盘的空间是从原有分区里分出来的。记得给 C 盘留些余地，Windows 更新、软件和日常文件都还需要空间。
3. **认准要操作的区域。** 下面以 C 盘为例，你电脑上的布局可能和截图不一样。标着“恢复”“EFI”等不熟悉的小分区，先不要删除或格式化。

如果是学校或公司的电脑，可以先问问管理员。操作时遇到看不懂的界面，或者发现磁盘有异常，也不用硬着头皮继续，先找熟悉磁盘管理的人帮忙看看。如果参考 AI 的建议，也记得核实后再操作，因为 AI 也可能出错。

## 第一步：从 C 盘腾出空间

在 Windows 搜索框中输入 **磁盘管理**，选择搜索结果中的**创建和格式化硬盘分区**。等待窗口加载后，在下方找到标有 `C:` 的区域，右键点击它，选择**压缩卷**。

![磁盘管理窗口中显示 C 盘和系统分区](img/windows-disk-management-marked.png)

稍等一会儿，Windows 会算出最多能腾出多少空间。输入你计划分给新分区的大小，单位是 MB。例如，`51200 MB` 约为 `50 GB`；这是演示数字，请根据自己的容量决定。确认输入的是“要腾出的大小”，而不是 C 盘最终保留的大小，然后点击**压缩**。

![压缩卷窗口中输入 51200 MB 的示例](img/windows-shrink-volume-marked.png)

完成后，磁盘管理中会出现一块标为**未分配**的空间。它还没有盘符，也不会立刻出现在“此电脑”中。

![C 盘旁出现 50 GB 未分配空间](img/windows-unallocated-marked.png)

![压缩 C 盘后出现未分配空间，再创建新卷](img/create-volume.png)

## 第二步：给新空间一个盘符

在刚出现的**未分配**空间上点击右键，选择**新建简单卷**，按照向导操作：

1. 确认新卷大小；如果希望全部使用刚腾出的空间，可以保留默认值。

   ![新建简单卷向导中的卷大小设置](img/windows-volume-size-marked.png)

2. 选择一个未被占用的盘符。D 盘已被使用也没关系，选其他字母即可。

   ![分配盘符页面，D 盘为修改后的示意](img/drive-letter-d-marked.png)

3. 按向导默认设置格式化这个**新建的空卷**，检查摘要，确认无误后点击**完成**。

   ![新建卷的格式化设置页面](img/windows-format-volume-marked.png)

格式化会清除目标卷上的数据，所以这里多看一眼：选中的是刚腾出的未分配空间，别选到 C 盘、其他数据盘或恢复分区。完成后打开“此电脑”，就能看到新的盘符。

![新卷创建完成，D 盘为修改后的示意](img/new-volume-d-example.png)

## 为什么没有腾出那么多空间？

如果你发现 C 盘明明还有不少空余，Windows 却不让你分出那么多，也不用太意外。部分系统文件无法自动移动，可能限制可压缩的大小。这时可以先按界面允许的范围操作，或者咨询了解磁盘管理的人；不要为了追求更大的数字随意删除系统文件。

新建分区后，原来的文件不会自动搬过去。你可以自己把需要整理的文件复制到新盘，确认能够打开后，再决定是否删除原文件。软件和系统文件则不要直接拖走。

## Mac 存储空间满了怎么办？

上面的操作适用于 Windows。Mac 通常不需要为了整理文件，照着 C 盘、D 盘的思路再分区。Mac 常用的 APFS 格式允许同一个容器中的多个宗卷共享空余空间，所以一般不用为了整理文件再单独分区。无论是增加宗卷还是分区，都不会让硬盘凭空变大。

如果 Mac 提示空间不足，可以先打开**苹果菜单 → 系统设置 → 通用 → 储存空间**，看看什么占用最多。再检查下载文件夹、卸载不用的应用，或者把不常用的大文件复制到外置硬盘；确认副本能打开后，再决定是否删除电脑里的原件。清空废纸篓前也先确认里面没有需要的文件。iCloud 储存空间优化是另一种选择，但需要留意云端容量和文件同步设置。

![macOS 储存空间设置](img/macos-storage-marked.png)

图中是英文界面，`General` 对应“通用”，`Storage` 对应“储存空间”。

分区说到底是为了让自己用得顺手。如果你现在靠文件夹就能整理得很好，继续这样用也完全可以。

## 参考资料

1. Microsoft Support, Disk Management in Windows: https://support.microsoft.com/en-gb/windows/experience/storage-filemanagement/disk-management-in-windows
2. Microsoft Learn, Shrink a Basic Volume: https://learn.microsoft.com/en-my/windows-server/storage/disk-management/shrink-a-basic-volume
3. Microsoft Support, Backup and restore with File History: https://support.microsoft.com/en-us/windows/experience/backup-recovery/backup-and-restore-with-file-history
4. Apple Support, Free up storage space on Mac: https://support.apple.com/en-gb/102624
5. Apple Support, Add, delete, or erase APFS volumes: https://support.apple.com/en-ie/guide/disk-utility/dskua9e6a110/mac
