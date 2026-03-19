# Multi-Agent Plan

本项目拆成 4 个代理，并行执行。每个代理必须写文件，不允许只在对话里汇报。

## Agent A - Research
职责：
- 搜集可信资料
- 记录事实、出处、图片来源、授权备注
- 形成 research/research.md
- 形成 research/assets_manifest.json
- 形成 research/source_log.md

## Agent B - Script
职责：
- 基于 research/research.md 写 60 秒中文脚本
- 拆成 6 个镜头
- 输出 script/script.md
- 输出 script/narration.txt
- 输出 script/subtitles.srt
- 输出 script/shotlist.json

## Agent C - Asset Builder
职责：
- 下载可用图片到 assets/images/
- 为缺失图示生成提示词到 assets/prompts/
- 如果已接图像/视频/TTS API，则生成素材到 assets/generated/、assets/audio/、assets/video_clips/
- 如果未接 API，也必须生成调用脚本和占位文件

## Agent D - Editor
职责：
- 用脚本化方式合成初版视频
- 优先使用 ffmpeg 或可重复执行的渲染流程
- 输出 output/final_v1.mp4
- 输出 output/review_checklist.md

## 全局规则
- 不允许编造学术事实
- 不允许跳过文件输出
- 每一步必须可复现
- 如果缺少 API key，不停止；改为输出可运行骨架
- 所有脚本默认 Python 3.11+
