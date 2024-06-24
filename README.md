Mangetsu 満月
Mangetsu 是一个工具集合，用于读取/写入 Nintendo Switch 版《月姬 重制版》中的数据格式。

构建
要构建所有工具，你至少需要以下依赖项：

sh
复制代码
sudo apt install -y build-essential cmake zlib1g-dev libssl-dev
如果你还希望构建图形工具，则需要一些额外的依赖项：

sh
复制代码
sudo apt install -y libopengl-dev libglfw3-dev
构建步骤：
sh
复制代码
git clone https://github.com/rschlaikjer/mangetsu.git
cd mangetsu
mkdir build && cd build
cmake ..                # 无 UI 程序
cmake -DBUILD_GUI=On .. # 包含 UI 程序
make
工具概览
MRG 文件
MRG 文件与 mrg/hed/nam 文件三元组一起操作。MRG 文件是归档格式，可以使用带有 mrg_ 前缀的工具进行解压/压缩。Nam 文件是可选的，当找到时将被使用。

mrg_info: 打印包含在 mrg 中的文件列表。可以选择输出机器可读格式。
mrg_extract: 解压 mrg 中的所有文件。如果存在 nam 文件，文件名将包含 nam 条目。
mrg_pack: 从单个文件构建一个新的 mrg/hed/nam。文件将按指定顺序打包。
mrg_replace: 给定一个基础 mrg/hed，创建一个新的 mrg/hed，其中原文件中某些偏移处的归档条目被新文件替换。
nam_read: 打印 nam 文件中的名称。
MZP 文件
与 MRG 文件类似，MZP 是包含多个部分的归档格式。与 MRG 不同，这些文件是自描述的，没有单独的 HED 文件。

mzp_info: 列出现有 mzp 文件的信息。
mzp_compress: 将多个文件组合成一个 mzp 归档。
mzp_extract: 从 mzp 归档中提取所有部分。
MZX
MZX 是一种基本的 LZ 相邻压缩格式。它仅是一种压缩格式，没有归档功能。

mzx_decompress: 解压缩 MZX 压缩的文件。
mzx_compress: 使用 MZX 压缩原始文件。注意：该程序目前不会尝试实际压缩 - 它将生成有效的 MZP 输出，但输出将比输入文件大。
NXX
NXGX / NXCX 文件是具有小头部的 GZIP / LZ 压缩数据格式。注意，由于缺少样本文件，NXCX 支持尚未测试。

nxx_decompress: 给定 NXGZ 或 NXCX 格式的文件，将数据解压缩到新文件。
nxgx_compress: 给定原始文件，以 NXGZ 格式压缩。
GUI 程序
如果启用了 GUI 支持，将构建 data_explorer 文件。此 UI 允许即时将文件重新解释为上述任何格式，以及递归提取和显示这些文件的子归档。它还具有十六进制视图和其他设计用于使原始格式分析更容易的工具。
