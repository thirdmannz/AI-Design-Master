# Contrast Rules (WCAG)

> 每個輸出的 token pair 必須通過下列硬性檢查。skill 在 Step 3 輸出前要跑 mental contrast check。

## 硬性最低門檻

| 用途 | 最低比例 | 標準 |
|------|---------|------|
| Body text on bg | 4.5:1 | WCAG AA |
| Large text (≥18pt 或 14pt bold) on bg | 3:1 | WCAG AA |
| UI components / borders / icons | 3:1 | WCAG AA non-text |
| AAA 目標（editorial/legal/finance） | 7:1 body, 4.5:1 large | WCAG AAA |

## 必檢 token pairs

skill 每個風格的 `:root` token 必須通過以下對比檢查：

| Pair | 最低 | 用途 |
|------|------|------|
| `--color-bg` × `--color-ink` | 7:1 | 主要 body text |
| `--color-bg` × `--color-muted` | 4.5:1 | 次要 text、metadata |
| `--color-bg` × `--color-accent` | 3:1 | Link、CTA text |
| `--color-accent` × `--color-bg-on-accent` | 4.5:1 | 按鈕內 text |
| `--color-rule` × `--color-bg` | 1.5:1 | Divider（非 text） |
| Focus ring × `--color-bg` | 3:1 | Focus indicator |

## Token 生成時的安全色公式

當 user 指定 accent 但對比不夠時：

```css
/* Light theme fallback */
--color-accent-text: color-mix(in oklch, var(--color-accent) 80%, black);
/* Dark theme fallback */
--color-accent-text-dark: color-mix(in oklch, var(--color-accent) 70%, white);
```

## Skill 自查清單（M5 rubric 對應）

- [ ] 所有 body text 對 bg ≥ 4.5:1
- [ ] 所有 large heading 對 bg ≥ 3:1
- [ ] Accent 色用在 text 時對 bg ≥ 3:1（非僅裝飾）
- [ ] Focus ring 對 bg ≥ 3:1
- [ ] Disabled state 仍可辨識（但允許 < 3:1）
- [ ] Dark mode 對應 token 也通過

## 工具

- 計算用 https://webaim.org/resources/contrastchecker/
- M5 視覺迴路會自動跑 axe-core
- OKLCH chroma 是比 HSL 更穩定的對比預測指標

## 風格特例

- **Brutalist**：用 pure black on pure white (21:1)，最高 contrast 是其視覺特徵
- **Glassmorphism**：blur card 上的 text 必須 bg 加 ≥ 60% opacity 黑底墊
- **Aurora UI**：gradient 背景上 text 必須有 fallback solid color，不能假設 gradient 任一點都通過
- **Magazine Longform**：drop cap 跟 body 同色，但 size 提供 hierarchy
- **Dark Luxury**：dark bg + 高 chroma accent 容易 fail，要降 saturation
