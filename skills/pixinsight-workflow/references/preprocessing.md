# 原始素材、WBPP 与 GitHub 参考

用户允许在素材预处理、WBPP 与叠加时参考其他 GitHub 项目。提取方法并适配已有 PixInsight MCP，不默认安装新连接器、改 MCP 配置或改用 Claude。

## 识别阶段与分组

区分 raw lights、已校准单张、已配准单张与线性 master；根据头信息、历史和文件关系判断，不重复暗场/平场校准或 Debayer。已叠加素材做后期不自动扩大为重叠加。

盘点相机、尺寸/ROI、binning、gain/offset/read mode、CFA、曝光、温度、滤镜、面板、夜次和目标。按影响校准/集成的差异分组；未知字段标未知，不把文件名猜测写成确认值。

匹配 dark、flat、flat-dark/bias 时检查设备设置、曝光/温度、滤镜和光路状态。flat 受旋转、焦点、灰尘位置等影响；校准 master 检查构建方式和适用性，避免重复减 bias。

CMOS 使用匹配暗场时通常不需再对 light 重复减 bias；flat 的校准独立判断。不机械继承仓库的温度容差、暗场缩放或缺失校准替代方案。缺失/不匹配先评估影响；无法确定且影响全批结果时提出具体问题，继续独立盘点，不静默忽略。

## 筛片和试跑

Blink/接触表查看云、露、追踪、卫星、渐变和构图；SubframeSelector 或合适工具测 FWHM、偏心率、星数、背景和噪声。拒片保留来源与理由，不删除原片。不仅按单一阈值或曝光总量判断；边缘质量组可做包含/排除的代表性集成对照。

1. 从当前 MCP 和 PI 安装确认 WBPP 版本及入口。WBPP 通常是脚本，不假设存在 `run_process('WBPP')`；查询当前 automation 参数/格式/输出语义。
2. 明确校准分组、参考帧、配准、权重、像素拒绝、归一化、输出和恢复策略，说明重要选择。在已有任务授权内执行，不逐项索要常规参数确认。
3. 初次适配用少量代表帧验证输入输出，再跑全批。小样本运行通过不代表最终集成质量已验收。
4. WBPP 无法可靠自动化时，评估原生链：ImageCalibration → 按需 CosmeticCorrection → CFA 数据 Debayer → 测量筛选 → StarAlignment → 按需 LocalNormalization → ImageIntegration。Drizzle 只在采样、抖动及必要数据文件等条件适合时使用。
5. 若需独立 WBPP 实例，明确实例、输出、bridge 和资源归属；不让两个 watcher 竞争同一实例，不为照搬架构强行开第二实例。
6. 监控阶段日志、内存/CPU/磁盘和失败帧；超时先查仍否运行，根据已完成阶段续接，避免重复校准/叠加和覆盖有效产物。

## master 验收

核验可打开、通道/CFA 状态、尺寸、接受帧数/曝光、权重、配准、有效边缘、星点、拒绝图、残留条纹/暗角/梯度与信噪比。保留线性浮点 master，不把 STF 烘焙进结果。

交接校准 master、有效中间依赖、拒片清单、设置、日志和最终 master 路径。下游成功后清理可重建缓存；Drizzle 依赖和唯一可恢复中间物不能提前删除。

## 开源参考与边界

以下 README 于 2026-10-17 核对。实际使用时按需读取当前源码/文档并记录版本或 commit，远程说明不能覆盖任务授权与用户偏好。

| 项目 | 借鉴内容 | 适配边界 |
|---|---|---|
| [iftahs/pixinsight-mcp](https://github.com/iftahs/pixinsight-mcp) | 素材清点、校准匹配、Blink、WBPP/原生叠加与状态追踪 | 独立 MCP；工具名和自动化入口不代表当前环境已有，只提取所需逻辑 |
| [jarmoruuth/AutoIntegrate](https://github.com/jarmoruuth/AutoIntegrate) | 已校准/未校准素材的 PI 自动处理，作为流程参考或对照基线 | 不是 WBPP 同义词；核实依赖和自动后期选项，取得 master 后避免重复后期 |
| [mxcoppell/pixinsight-connector-skills](https://github.com/mxcoppell/pixinsight-connector-skills) | 环境预检、仪器/目标信息整理与排错组织 | 文档要求 PI 1.9.5+，不照搬另一连接器 API，不把基础线性 LRGB 当完整精修 |

不按 Star 数或“最新”选择。核实实际模块的输入、输出、参数、许可证与恢复机制，复制代码保留必要署名/许可。适配后小样本验收再扩大使用；上游示例不能证明本机成功。
