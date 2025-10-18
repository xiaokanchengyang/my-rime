# Xiaohe Shuangpin · Wanxiang Dictionary (Arch Linux / fcitx5-rime / ibus-rime)

Only Xiaohe Shuangpin is kept. Wanxiang dictionaries, grammar and Lua features are integrated. All other input methods are removed, filenames are clear and minimal.

## Tree

```
rime/
  ├─ xiaohe_shuangpin_wanxiang.schema.yaml  # schema: Xiaohe + Wanxiang
  ├─ default.yaml                           # schema list (Wanxiang compatible)
  ├─ default.custom.yaml                    # override: enable this schema only
  ├─ wanxiang.custom.yaml                   # force Xiaohe algebra only
  ├─ wanxiang.dict.yaml                     # Wanxiang main dictionary (split in dicts/)
  ├─ wanxiang_algebra.yaml                  # Wanxiang algebra (includes Xiaohe section)
  ├─ wanxiang_symbols.yaml                  # Wanxiang symbols
  ├─ wanxiang_reverse.*                     # reverse/chaifen
  ├─ wanxiang_charset.*                     # charset filter
  ├─ wanxiang_mixedcode.*                   # mixed code (en+zh)
  ├─ dicts/                                 # tables (chars/base/correlation/...)
  ├─ lua/                                   # Wanxiang Lua extensions
  ├─ opencc/                                # OpenCC data
  └─ custom/                                # reserved for user customization
```

## Install

- fcitx5-rime (recommended)
  - user dir: `~/.local/share/fcitx5/rime`
- ibus-rime
  - user dir: `~/.config/ibus/rime`

Steps:
1. Backup your existing user dir (if any).
2. Copy the `rime/` folder here into your user dir.
3. Redeploy:
   - fcitx5: choose "Redeploy" from the tray icon menu, or run `fcitx5-remote -r`.
   - ibus: `ibus-daemon -rd` or redeploy in settings UI.
4. Select schema "`小鹤双拼·万象词库`" from the schema switcher.

## Xiaohe only

- `wanxiang.custom.yaml` sets:
  - `wanxiang_algebra:/base/小鹤双拼`
- `default.custom.yaml` enables only `xiaohe_shuangpin_wanxiang`.
- All in-schema switches to other layouts are removed.

## Notes

- Tones: `7/8/9/0` represent tone `1/2/3/4`; neutral tone merges into 4.
- Reverse lookup / decomposition: press backtick `` ` `` to enter.
- Date/Time/Calendar etc.: use `/sj`, `/rq`, `/nl`, etc. (see upstream docs).
- Mixed code and English: type directly (`wanxiang_mixedcode`).
- Wrap first candidate with paired symbols: type text, then `\` + mapping key.

## Customize

- Fixed packs: place `userxx.dict.yaml` in user root and enable `translator/packs` in `wanxiang.custom.yaml`.
- Custom phrases: edit `custom_phrase.txt` (will be prioritized).
- See upstream `rime_wanxiang` README for advanced Lua/tips/features.

## Upstream

- Base: `amzxyz/rime_wanxiang` (dictionaries/grammar/lua/symbols/opencc)
- Layout: Xiaohe Shuangpin (参考 `ASC8384/myRime` and `ScriptGo/rime`)

## FAQ

- Schema not showing: ensure files are placed in the correct user dir and redeployed.
- Performance: Wanxiang is large; first deploy may take time.
- Xiaohe-only: switching to other layouts is intentionally disabled; change `wanxiang.custom.yaml` manually if needed.
