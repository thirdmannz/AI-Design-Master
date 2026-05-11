# Keyboard Navigation

> 滑鼠不能做的，鍵盤必須做得到。每個輸出都要鍵盤可走完。

## 基本要求

1. **所有互動元件鍵盤可達** — Tab 可走到，Shift+Tab 可走回
2. **Tab order = 視覺 order** — 不用 `tabindex > 0` 改順序，調 DOM
3. **Enter / Space 觸發** — Button: Enter+Space；Link: Enter
4. **ESC 關閉** — Modal、dropdown、tooltip
5. **Arrow keys** — Tab list、menu、radio group 內部導覽
6. **Skip link** — 跳過 nav 直接到 main，必出

## 預設快捷鍵對照

| 元件 | 鍵 | 行為 |
|------|----|------|
| Button | Enter / Space | 觸發 |
| Link | Enter | 跳轉 |
| Checkbox | Space | toggle |
| Radio | Arrow Up/Down | 切選項 + 自動 select |
| Select native | Arrow + Enter | 開合 + 選 |
| Tabs | Arrow Left/Right | 切 tab（不 Tab 鍵） |
| Menu | Arrow Up/Down, Esc | 切 item + 關閉 |
| Modal | Esc, Tab (trap) | 關閉 + focus trap |
| Details/Summary | Enter / Space | 展開 |
| Slider | Arrow Left/Right | -/+ 一格 |
| Date picker | Arrow + Page Up/Down | 切日/月 |
| Search combobox | Arrow + Enter | 選 suggestion |

## Skip link 標準寫法

```html
<a href="#main" class="skip-link">Skip to main content</a>
```
```css
.skip-link {
  position: absolute;
  top: -100px;
  left: 0;
  background: var(--color-bg);
  color: var(--color-ink);
  padding: 0.75rem 1rem;
  z-index: 100;
  text-decoration: underline;
  transition: top 0.2s;
}
.skip-link:focus {
  top: 0;
}
```

## Focus trap (modal)

Native `<dialog>` 自動 trap。自製 modal 必須：

1. 開啟時記住觸發 element，焦點移到 modal
2. Tab 走到最後一個 element 後跳回第一個
3. Shift+Tab 走到第一個後跳回最後
4. ESC 關閉，焦點還給觸發 element

## 常見 anti-patterns（禁用）

- ❌ `tabindex="0"` on `<div role="button">` — 改用 `<button>`
- ❌ `tabindex="-1"` 在所有 focusable — 破壞鍵盤導覽
- ❌ `tabindex > 0` — 全部變成 1 = 順序錯亂
- ❌ Disabling Tab key with JS — 永遠禁止
- ❌ Modal open 後焦點沒移進 modal — 失靈
- ❌ Dropdown open 後焦點沒移到第一個 item
- ❌ 用 onClick 在 `<div>` 上 — 鍵盤不能觸發

## Skill 自查

- [ ] 一定有 skip link 在頁首
- [ ] Tab order 從上到下、從左到右
- [ ] 沒有 `tabindex > 0`
- [ ] Modal / dropdown 鍵盤可關（ESC）
- [ ] Tabs 用 Arrow 切換（不是 Tab）
- [ ] 所有 互動元素 hover state ⊆ focus state（focus 也要看得到）
- [ ] Form submit 用 Enter 在任一 input 都可觸發
- [ ] 鍵盤走完全頁無 dead-end（焦點消失或 trap 在區域內）

## 測試方法

1. **拔滑鼠**：只用 Tab/Shift+Tab/Enter/Space/Arrow/ESC，走完整個頁面
2. **盲走**：閉上眼睛，用語音知道現在 focus 在哪
3. **devtools**：Chrome DevTools → Accessibility → Show Tab Order
