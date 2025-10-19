# 小鹤双拼 · 万象词库（Arch Linux / fcitx5-rime / ibus-rime）

只保留小鹤双拼，整合万象词库与其 Lua 扩展，精简无关方案与文件，命名清晰可维护。

## 目录结构

```
rime/
  ├─ xiaohe_shuangpin_wanxiang.schema.yaml  # 方案：小鹤双拼 + 万象
  ├─ default.yaml                           # 方案清单（包含 wanxiang 兼容设置）
  ├─ default.custom.yaml                    # 覆盖，仅启用本方案
  ├─ wanxiang.custom.yaml                   # 仅指定小鹤双拼转写
  ├─ wanxiang.dict.yaml                     # 万象主词库（按表拆分见 dicts/）
  ├─ wanxiang_algebra.yaml                  # 万象转写（含“小鹤双拼”段落）
  ├─ wanxiang_symbols.yaml                  # 万象符号表
  ├─ wanxiang_reverse.*                     # 反查/拆分相关
  ├─ wanxiang_charset.*                     # 字符集过滤
  ├─ wanxiang_mixedcode.*                   # 中英混合
  ├─ dicts/                                 # 词库分表（chars/base/correlation/...）
  ├─ lua/                                   # 万象 Lua 扩展
  ├─ opencc/                                # OpenCC 词表
  └─ custom/                                # 预留自定义目录
```

## 安装

- fcitx5-rime（推荐）
  - 用户目录：`~/.local/share/fcitx5/rime`
- ibus-rime
  - 用户目录：`~/.config/ibus/rime`

步骤：
1. 备份你的原有用户目录（若有）。
2. 将本仓库下的 `rime/` 目录完整复制到你的 Rime 用户目录。
3. 重新部署：
   - fcitx5：在状态栏图标菜单选择“重新部署”，或运行 `fcitx5-remote -r`。
   - ibus：`ibus-daemon -rd` 或在设置中重新部署。
4. 在方案选单中选择“`小鹤双拼·万象词库`”。

## 仅保留小鹤双拼

- 已在 `wanxiang.custom.yaml` 中强制使用：
  - `wanxiang_algebra:/base/小鹤双拼`
- 已替换默认方案列表为：
  - `default.custom.yaml` -> 仅 `xiaohe_shuangpin_wanxiang`
- 已移除其他双拼/全拼切换脚本入口，不会误切换为其他键位方案。

## 使用要点

- 声调数字：`7/8/9/0` 分别代表 `1/2/3/4` 声；轻声归并 4 声。
- 反查/拆分：输入反引号 `` ` `` 进入，继续输入部件或笔画。
- 日期/时间/节气等：输入 `/sj`、`/rq`、`/nl` 等（详见万象 README）。
- 混合编码与英文：无需切换，直接输入（`wanxiang_mixedcode`）。
- 快符包裹首选：先输入词，再输入反斜杠 `\` + 映射键。

## 自定义

- 自定义固定词典：将 `userxx.dict.yaml` 放在用户根目录，并在 `wanxiang.custom.yaml` 中 `translator/packs` 打开注释。
- 自定义短语：编辑 `custom_phrase.txt`（存在则优先显示）。
- 详尽功能、Lua 快捷键、Tips 请阅读 `rime_wanxiang` 上游文档。

## 依赖与来源

- 基础：`amzxyz/rime_wanxiang`（词库/语法/Lua/符号/OpenCC）
- 键位：小鹤双拼（`ASC8384/myRime` 与 `ScriptGo/rime` 参考）

## 常见问题

- 方案未出现：确认复制到了正确的“用户目录”；确保重新部署成功。
- 性能与占用：万象词库较大，首次部署耗时较长，耐心等待。
- 只要小鹤：已去除切换入口，如需临时测试其他方案，请手动修改 `wanxiang.custom.yaml`。
