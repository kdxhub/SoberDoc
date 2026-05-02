---
layout: default
---

# Sober UI 组件文档

Sober 是一个基于 Web Components 的轻量级 UI 库，提供 Material Design 3 风格的组件。所有组件均以 `<s-*>` 自定义元素的形式使用，支持声明式属性、插槽（slot）和 JavaScript 交互。

> [@] 本文档有 AI 参与编辑部分。

> [x] 这不是官方文档。

> [i] [Github 仓库](https://github.com/kdxhub/SoberDoc)

---

## 目录

- [Alert](#alert)
- [Appbar](#appbar)
- [Avatar](#avatar)
- [Badge](#badge)
- [BottomSheet](#bottomsheet)
- [Button](#button)
- [Card](#card)
- [Carousel / CarouselItem](#carousel--carouselitem)
- [Checkbox](#checkbox)
- [Chip](#chip)
- [CircularProgress](#circularprogress)
- [Date](#date)
- [DatePicker](#datepicker)
- [Dialog](#dialog)
- [Divider](#divider)
- [Drawer](#drawer)
- [Empty](#empty)
- [FAB](#fab)
- [Field](#field)
- [Fold](#fold)
- [Icon](#icon)
- [IconButton](#iconbutton)
- [LinearProgress](#linearprogress)
- [Menu / MenuItem](#menu--menuitem)
- [Navigation / NavigationItem](#navigation--navigationitem)
- [Page](#page)
- [Pagination](#pagination)
- [Picker / PickerItem](#picker--pickeritem)
- [Popup](#popup)
- [PopupMenu / PopupMenuItem](#popupmenu--popupmenuitem)
- [RadioButton](#radiobutton)
- [Rate](#rate)
- [Ripple](#ripple)
- [ScrollView](#scrollview)
- [Search](#search)
- [SegmentedButton / SegmentedButtonItem](#segmentedbutton--segmentedbuttonitem)
- [Skeleton](#skeleton)
- [Slider](#slider)
- [Snackbar](#snackbar)
- [Switch](#switch)
- [Tab / TabItem](#tab--tabitem)
- [Table / Thead / Tbody / Tr / Th / Td](#table--thead--tbody--tr--th--td)
- [TextField](#textfield)
- [Tooltip](#tooltip)

---

## Alert

### `<s-alert>`

用于显示信息提示条。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `"info"` \| `"success"` \| `"warning"` \| `"error"` | `"info"` | 提示类型，影响颜色和图标 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前置图标（可替换默认 SVG） |
| (默认) | 提示文本 |
| `end` | 后置操作区域，如按钮 |

**用法示例**

```html
<s-alert type="success">操作成功</s-alert>

<s-alert type="error">
  发生错误
  <s-button slot="end" type="text">重试</s-button>
</s-alert>
```

**JavaScript 交互**

```js
const alert = document.querySelector('s-alert');
alert.type = 'warning';
```

---

## Appbar

### `<s-appbar>`

顶部导航栏容器，支持响应式布局。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 最左侧内容 |
| `navigation` | 导航图标（如汉堡菜单） |
| `logo` | logo 图片或图标 |
| `headline` | 标题文本 |
| (默认) | 中间区域（通常放置其他操作） |
| `search` | 搜索组件（`<s-search>`），在小屏幕下会拉伸 |
| `action` | 操作区域按钮 |
| `end` | 最右侧内容 |

**用法示例**

```html
<s-appbar>
  <s-icon-button slot="navigation" name="menu"></s-icon-button>
  <span slot="headline">My App</span>
  <s-search slot="search" placeholder="搜索..."></s-search>
  <s-icon-button slot="action" name="dark_mode"></s-icon-button>
</s-appbar>
```

**响应式行为**

- 窗口宽度 `≤1024px` 时高度变为 56px
- 窗口宽度 `≤768px` 时搜索框自动伸展

---

## Avatar

### `<s-avatar>`

头像组件，支持图片或图标显示，可叠加徽章。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `src` | `string` | `""` | 头像图片 URL |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 当没有图片时显示自定义内容（如文本或图标） |
| `badge` | 右下角徽章，通常放置 `<s-badge>` |

**事件**

| 事件名 | 说明 |
|--------|------|
| `load` | 图片加载成功时触发 |
| `error` | 图片加载失败时触发 |

**用法示例**

```html
<s-avatar src="user.jpg"></s-avatar>

<s-avatar>
  <s-icon name="person"></s-icon>
  <s-badge slot="badge">3</s-badge>
</s-avatar>
```

**JavaScript 交互**

```js
const avatar = document.querySelector('s-avatar');
avatar.addEventListener('load', () => console.log('头像加载完成'));
avatar.src = 'new-avatar.jpg';
```

---

## Badge

### `<s-badge>`

徽章提示，用于显示数量或状态点。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 徽章内容，为空时显示为小圆点 |

**用法示例**

```html
<!-- 小圆点 -->
<s-badge></s-badge>

<!-- 显示数字 -->
<s-badge>5</s-badge>

<!-- 嵌入 IconButton -->
<s-icon-button>
  <s-icon name="notifications"></s-icon>
  <s-badge slot="badge">9+</s-badge>
</s-icon-button>
```

---

## BottomSheet

### `<s-bottom-sheet>`

底部弹出面板，支持手势关闭。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `showed` | `boolean` | `false` | 是否显示 |
| `disabledGesture` | `boolean` | `false` | 禁用手势关闭 |

**事件**

| 事件名 | 类型 | 说明 |
|--------|------|------|
| `show` | `CustomEvent` (可取消) | 显示前触发，`detail.source` 为触发来源 (`"TRIGGER"`) |
| `showed` | `Event` | 显示动画完成后触发 |
| `close` | `CustomEvent` (可取消) | 关闭前触发，`detail.source` 为触发来源 (`"SCRIM"`, `"GESTURE"`) |
| `closed` | `Event` | 关闭动画完成后触发 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 点击触发展开的元素 |
| `text` | 固定文本区域（带内边距） |
| (默认) | 主要滚动内容区域 |

**静态方法**

`BottomSheet.builder(options)`

快速创建一个 BottomSheet 并附加到页面中，返回组件实例。`options` 支持：
- `root` : 父容器（默认为 document.body 或 `<s-page>`）
- `view` : 内容（字符串、HTMLElement 或函数 `(bottomSheet) => {}`）
- `disabledGesture` : 禁用手势

**用法示例**

```html
<s-bottom-sheet id="sheet">
  <s-button slot="trigger">打开</s-button>
  <div style="padding:24px">底部内容</div>
</s-bottom-sheet>
```

**JavaScript 交互**

```js
// 编程式创建
BottomSheet.builder({ view: '这是底部面板' });

// 控制已有实例
const sheet = document.getElementById('sheet');
sheet.showed = true;
sheet.addEventListener('closed', () => console.log('面板已关闭'));
```

---

## Button

### `<s-button>`

按钮组件，支持多种样式变体。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `"filled"` \| `"elevated"` \| `"filled-tonal"` \| `"outlined"` \| `"text"` | `"filled"` | 按钮样式 |
| `disabled` | `boolean` | `false` | 禁用状态 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标 |
| (默认) | 按钮文本 |
| `end` | 后缀图标 |

**用法示例**

```html
<s-button>默认按钮</s-button>

<s-button type="outlined">
  <s-icon slot="start" name="add"></s-icon>
  带图标
</s-button>

<s-button type="text" disabled>文本禁用</s-button>
```

**JavaScript 交互**

```js
const btn = document.querySelector('s-button');
btn.addEventListener('click', () => console.log('点击按钮'));
btn.disabled = true;
```

---

## Card

### `<s-card>`

卡片容器，支持图片、标题、操作等布局。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `"elevated"` \| `"filled"` \| `"outlined"` | `"elevated"` | 卡片样式 |
| `clickable` | `boolean` | `false` | 是否可点击，启用涟漪和悬浮阴影 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 卡片最顶部自定义内容 |
| `image` | 图片区域 |
| `headline` | 主标题 |
| `subhead` | 副标题 |
| `text` | 正文 |
| (默认) | 其他正文区域 |
| `action` | 操作按钮区域 |
| `end` | 卡片底部自定义内容 |

**用法示例**

```html
<s-card clickable>
  <img slot="image" src="cover.jpg" alt="">
  <div slot="headline">卡片标题</div>
  <div slot="subhead">副标题</div>
  <div slot="text">这是一段描述文本。</div>
  <s-button slot="action" type="text">操作</s-button>
</s-card>
```

---

## Carousel / CarouselItem

### `<s-carousel>`

轮播图组件，管理子项 `<s-carousel-item>`。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 当前选中项的 `value` 属性值 |
| `autoplay` | `boolean` | `false` | 是否自动播放 |
| `duration` | `number` | `4000` | 自动播放间隔（毫秒） |

**暴露的属性/方法（通过 JavaScript 访问实例）**

| 成员 | 类型 | 说明 |
|------|------|------|
| `options` | `CarouselItem[]` | 所有轮播项数组 |
| `selectedIndex` | `number` | 当前选中索引 |
| `togglePrevious()` | `function` | 切换到上一项 |
| `toggleNext()` | `function` | 切换到下一项 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 轮播项切换时触发 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 放置 `<s-carousel-item>` |

---

### `<s-carousel-item>`

轮播项。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `selected` | `boolean` | `false` | 是否当前选中 |
| `value` | `string` | `""` | 该项的值，用于 `value` 匹配 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 轮播项内容 |

**用法示例**

```html
<s-carousel autoplay duration="3000">
  <s-carousel-item>
    <img src="slide1.jpg" style="width:100%;height:100%;object-fit:cover">
  </s-carousel-item>
  <s-carousel-item>
    <div style="background:#4CAF50;height:100%;display:flex;align-items:center;justify-content:center">Slide 2</div>
  </s-carousel-item>
  <s-carousel-item>
    <img src="slide3.jpg" style="width:100%;height:100%;object-fit:cover">
  </s-carousel-item>
</s-carousel>
```

**JavaScript 交互**

```js
const carousel = document.querySelector('s-carousel');
carousel.toggleNext();
carousel.addEventListener('change', () => {
  console.log('当前索引:', carousel.selectedIndex);
});
```

---

## Checkbox

### `<s-checkbox>`

复选框组件，支持不确定状态。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | `false` | 是否选中 |
| `indeterminate` | `boolean` | `false` | 不确定状态（优先级高于 checked） |
| `disabled` | `boolean` | `false` | 是否禁用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `unchecked` | 未选中时的图标（可自定义 SVG） |
| `checked` | 选中时的图标 |
| `indeterminate` | 不确定状态图标 |
| (默认) | 标签文本 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 点击切换后触发 |

**用法示例**

```html
<s-checkbox>同意协议</s-checkbox>
<s-checkbox checked>默认选中</s-checkbox>
<s-checkbox indeterminate>部分选中</s-checkbox>
<s-checkbox disabled>禁用</s-checkbox>
```

**JavaScript 交互**

```js
const cb = document.querySelector('s-checkbox');
cb.checked = true;
cb.addEventListener('change', () => {
  console.log(cb.checked); // true/false
});
```

---

## Chip

### `<s-chip>`

标签/碎片组件，常用于过滤器或输入标签。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `"filled"` \| `"outlined"` | `"filled"` | 样式 |
| `checked` | `boolean` | `false` | 选中状态 |
| `clickable` | `boolean` | `false` | 是否可点击切换选中 |
| `disabled` | `boolean` | `false` | 禁用 |
| `value` | `string` | `""` | 值 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标/头像 |
| (默认) | 文本内容 |
| `end` | 后缀图标 |
| `action` | 操作按钮（如关闭），点击不会触发 chip 的切换 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 点击切换选中状态后触发（`clickable` 为 true 时） |

**用法示例**

```html
<s-chip>标签</s-chip>

<s-chip clickable checked>
  <s-avatar slot="start" src="avatar.jpg"></s-avatar>
  用户名
</s-chip>

<s-chip type="outlined">
  可移除
  <s-icon-button slot="action" name="close"></s-icon-button>
</s-chip>
```

---

## CircularProgress

### `<s-circular-progress>`

圆形进度指示器。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | `0` | 当前进度值 |
| `max` | `number` | `100` | 最大值 |
| `indeterminate` | `boolean` | `false` | 是否不确定模式（持续旋转） |
| `animated` | `boolean` | `false` | 启用过渡动画（当值变化时） |

**用法示例**

```html
<!-- 不确定进度 -->
<s-circular-progress indeterminate></s-circular-progress>

<!-- 确定进度 -->
<s-circular-progress value="65" animated></s-circular-progress>
```

**JavaScript 交互**

```js
const progress = document.querySelector('s-circular-progress');
progress.value = 75;
```

---

## Date

### `<s-date>`

日期选择日历面板（不含弹出层，常被 DatePicker 内部使用）。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 选中的日期字符串（如 `"2025-03-15"`） |
| `min` | `string` | `"1900-01-01"` | 最小日期 |
| `max` | `string` | `"2099-12-31"` | 最大日期 |
| `locale` | `string` | `""` | 本地化代码（如 `"zh"`, `"en"`） |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `headline` | 顶部自定义标题 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 选中日期后触发 |

**静态方法**

- `Date.addLocale(locale, config)` - 注册本地化语言，`config` 形如：
  ```js
  {
    display: (date) => `...`,       // 格式：星期五, 3月14日
    displayMonth: (date) => `...`,  // 格式：2025年3月
    displayWeeks: ['日','一','二','三','四','五','六']
  }
  ```
- `Date.setLocale(locale)` - 设置当前全局语言

**用法示例**

```html
<s-date value="2025-03-14"></s-date>
```

**JavaScript 交互**

```js
const dateEl = document.querySelector('s-date');
dateEl.value = '2025-06-01';
dateEl.addEventListener('change', () => console.log(dateEl.value));
```

---

## DatePicker

### `<s-date-picker>`

日期选择器（弹出式），基于 `<s-dialog>` 和 `<s-date>`。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 当前选中日期 |
| `label` | `string` | `""` | 标签文本（未选择时显示） |
| `format` | `string` | `"yyyy-MM-dd"` | 日期显示格式 |
| `positiveText` | `string` | `"确定"` | 确认按钮文本 |
| `negativeText` | `string` | `"取消"` | 取消按钮文本 |
| `min` | `string` | `""` | 最小日期 |
| `max` | `string` | `""` | 最大日期 |
| `locale` | `string` | `""` | 本地化代码 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 自定义触发器（默认显示一个输入框样式的字段） |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 确认选中后触发 |

**用法示例**

```html
<s-date-picker label="选择日期" format="yyyy/MM/dd"></s-date-picker>

<s-date-picker>
  <s-button slot="trigger" type="outlined">
    <s-icon slot="start" name="calendar"></s-icon>
    选择日期
  </s-button>
</s-date-picker>
```

**JavaScript 交互**

```js
const picker = document.querySelector('s-date-picker');
picker.addEventListener('change', () => console.log(picker.value));
```

---

## Dialog

### `<s-dialog>`

对话框组件。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `showed` | `boolean` | `false` | 是否显示 |
| `size` | `"standard"` \| `"full"` | `"standard"` | 对话框尺寸 |

**事件**

| 事件名 | 类型 | 说明 |
|--------|------|------|
| `show` | `CustomEvent` (可取消) | 显示前触发 |
| `showed` | `Event` | 显示动画完成后 |
| `close` | `CustomEvent` (可取消) | 关闭前触发，`detail.source` 为 `"SCRIM"` 或 `"ACTION"` |
| `closed` | `Event` | 关闭动画完成后 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 触发按钮 |
| `headline` | 标题 |
| (默认) | 正文区域（可滚动） |
| `text` | 文本区域（固定内边距） |
| `action` | 操作按钮区域 |
| `custom` | 完全自定义弹出内容（替换默认容器） |

**静态方法**

`Dialog.builder(options)`

快速创建对话框，返回实例。`options` 支持：
- `root` : 父容器
- `headline` : 标题
- `text` : 正文文本
- `view` : 自定义内容（HTMLElement 或 `(dialog) => {}`）
- `actions` : 按钮数组，每项 `{ text, click }`

**用法示例**

```html
<s-dialog id="dlg">
  <s-button slot="trigger">打开对话框</s-button>
  <div slot="headline">标题</div>
  <div slot="text">内容描述...</div>
  <s-button slot="action" type="text">取消</s-button>
  <s-button slot="action" type="text">确定</s-button>
</s-dialog>
```

**JavaScript 交互**

```js
// 编程式创建
Dialog.builder({
  headline: '提示',
  text: '确认删除吗？',
  actions: [
    { text: '取消' },
    { text: '确定', click: () => console.log('删除') }
  ]
});

// 手动控制
const dialog = document.getElementById('dlg');
dialog.showed = true;
dialog.addEventListener('close', e => {
  console.log('关闭来源:', e.detail.source);
});
```

---

## Divider

### `<s-divider>`

分割线，可包含文本。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 文本（可选） |

**用法示例**

```html
<s-divider></s-divider>
<s-divider>或</s-divider>
```

---

## Drawer

### `<s-drawer>`

抽屉导航容器，支持侧边栏滑入效果（左右两侧）。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 主体内容区域 |
| `start` | 左侧抽屉内容 |
| `end` | 右侧抽屉内容 |

**暴露的方法（通过 JavaScript 访问实例）**

| 方法 | 说明 |
|------|------|
| `show(side)` | 显示抽屉，`side` 为 `"start"` 或 `"end"` |
| `close(side)` | 关闭抽屉 |
| `toggle(side)` | 切换显示状态 |

在 ≤1024px 的屏幕上，抽屉会变为临时模式（覆盖显示，带半透明遮罩）；更大屏幕则为持久模式。

**用法示例**

```html
<s-drawer>
  <div slot="start">
    <s-menu>
      <s-menu-item>菜单1</s-menu-item>
      <s-menu-item>菜单2</s-menu-item>
    </s-menu>
  </div>
  <s-appbar>
    <s-icon-button slot="navigation" onclick="this.closest('s-drawer').toggle('start')" name="menu"></s-icon-button>
    <span slot="headline">页面</span>
  </s-appbar>
  <div style="padding:20px">主内容</div>
</s-drawer>
```

**JavaScript 交互**

```js
const drawer = document.querySelector('s-drawer');
drawer.show('start');
drawer.close('end');
```

---

## Empty

### `<s-empty>`

空状态占位图。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `icon` | 自定义图标（默认是空盒子 SVG） |
| (默认) | 提示文本 |

**用法示例**

```html
<s-empty>暂无数据</s-empty>
```

---

## FAB

### `<s-fab>`

浮动操作按钮（Floating Action Button）。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `hidden` | `boolean` | `false` | 是否隐藏（缩小动画） |
| `disabled` | `boolean` | `false` | 是否禁用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标 |
| (默认) | 按钮文本或图标 |
| `end` | 后缀图标 |

**用法示例**

```html
<s-fab>
  <s-icon name="add"></s-icon>
</s-fab>

<s-fab>
  <s-icon slot="start" name="edit"></s-icon>
  编辑
</s-fab>
```

**JavaScript 交互**

```js
const fab = document.querySelector('s-fab');
fab.hidden = true;
```

---

## Field

### `<s-field>`

输入字段容器，为 `TextField` 等组件提供 Material Design 3 风格的边框、标签动画。通常不单独使用，而是作为内部依赖。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `focused` | `boolean` | `false` | 聚焦状态（边框高亮） |
| `fixed` | `boolean` | `true` | 标签是否浮动（`false` 时标签居中） |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导装饰 |
| (默认) | 视图区域（输入元素等） |
| `label` | 标签文本 |
| `end` | 后缀装饰 |
| `custom` | 自定义覆盖内容（如 Ripple） |

一般不直接使用，而是由 `TextField`、`Picker`、`DatePicker` 等组合使用。

---

## Fold

### `<s-fold>`

折叠/展开面板。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `folded` | `boolean` | `false` | 是否折叠 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 触发器（点击切换折叠） |
| (默认) | 折叠的内容区域 |

**用法示例**

```html
<s-fold>
  <s-button slot="trigger">展开/折叠</s-button>
  <div>折叠内容...</div>
</s-fold>
```

**JavaScript 交互**

```js
const fold = document.querySelector('s-fold');
fold.folded = false;
```

---

## Icon

### `<s-icon>`

图标组件，支持内置图标名称或外部 SVG/图片。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | 内置图标名 | - | 内置图标名称（见下方列表） |
| `src` | `string` | `""` | 外部 SVG 或图片 URL |

内置图标名称包括：`home`, `add`, `search`, `menu`, `arrow_back`, `arrow_forward`, `arrow_upward`, `arrow_downward`, `arrow_drop_up`, `arrow_drop_down`, `arrow_drop_left`, `arrow_drop_right`, `more_vert`, `more_horiz`, `close`, `done`, `chevron_up`, `chevron_down`, `chevron_left`, `chevron_right`, `light_mode`, `dark_mode`, `star`, `favorite` 等。

**事件**

| 事件名 | 说明 |
|--------|------|
| `load` | 图标资源加载成功（src 模式） |
| `error` | 加载失败 |

**用法示例**

```html
<s-icon name="search"></s-icon>
<s-icon src="custom-icon.svg"></s-icon>
```

**JavaScript 交互**

```js
const icon = document.querySelector('s-icon');
icon.name = 'done';
icon.addEventListener('load', () => console.log('图标已加载'));
```

---

## IconButton

### `<s-icon-button>`

图标按钮。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `"standard"` \| `"filled"` \| `"filled-tonal"` \| `"outlined"` | `"standard"` | 按钮变体 |
| `disabled` | `boolean` | `false` | 禁用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导内容 |
| (默认) | 主要图标（通常是 `<s-icon>` 或 SVG） |
| `end` | 后缀内容 |
| `badge` | 徽章（如 `<s-badge>`） |

**用法示例**

```html
<s-icon-button name="search"></s-icon-button>

<s-icon-button type="filled">
  <s-icon name="favorite"></s-icon>
</s-icon-button>

<s-icon-button>
  <svg viewBox="0 0 24 24"><path d="..."/></svg>
  <s-badge slot="badge">3</s-badge>
</s-icon-button>
```

---

## LinearProgress

### `<s-linear-progress>`

线性进度条。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | `0` | 进度值 |
| `max` | `number` | `100` | 最大值 |
| `indeterminate` | `boolean` | `false` | 不确定模式 |
| `animated` | `boolean` | `false` | 进度变化动画 |

**用法示例**

```html
<s-linear-progress value="30" animated></s-linear-progress>
<s-linear-progress indeterminate></s-linear-progress>
```

---

## Menu / MenuItem

### `<s-menu>`

菜单容器，通常与 `<s-menu-item>` 配合使用。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `label` | 菜单组标题 |
| (默认) | `<s-menu-item>` 列表 |

---

### `<s-menu-item>`

菜单项，支持嵌套子菜单。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | `false` | 选中高亮 |
| `folded` | `boolean` | `true` | 子菜单折叠状态 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标 |
| (默认) | 菜单项文本 |
| `end` | 后缀图标（默认有一个展开箭头） |
| `menu` | 子菜单内容（可嵌套 `<s-menu>`） |

**用法示例**

```html
<s-menu>
  <s-menu-item checked>首页</s-menu-item>
  <s-menu-item>消息</s-menu-item>
  <s-menu-item folded>
    设置
    <s-menu slot="menu">
      <s-menu-item>个人资料</s-menu-item>
      <s-menu-item>账号安全</s-menu-item>
    </s-menu>
  </s-menu-item>
</s-menu>
```

**JavaScript 交互**

```js
const item = document.querySelector('s-menu-item');
item.checked = true;
item.folded = false; // 展开子菜单
```

---

## Navigation / NavigationItem

### `<s-navigation>`

底部导航栏或侧边导航栏容器。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `mode` | `"bottom"` \| `"rail"` | `"bottom"` | 导航模式（底部或侧栏） |
| `value` | `string` | `""` | 当前选中项的值（与 NavigationItem 的 `value` 匹配） |

**暴露的成员**

| 成员 | 类型 | 说明 |
|------|------|------|
| `options` | `NavigationItem[]` | 所有导航项 |
| `selectedIndex` | `number` | 当前选中索引 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 导航栏顶部/起始内容 |
| (默认) | `<s-navigation-item>` 列表 |
| `end` | 导航栏底部/末尾内容 |

---

### `<s-navigation-item>`

导航项。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `selected` | `boolean` | `false` | 是否选中 |
| `value` | `string` | `""` | 标识值 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `icon` | 图标（通常放 `<s-icon>`） |
| `badge` | 徽章 |
| `text` | 文本标签 |

**用法示例**

```html
<s-navigation value="home">
  <s-navigation-item value="home" selected>
    <s-icon slot="icon" name="home"></s-icon>
    <span slot="text">首页</span>
  </s-navigation-item>
  <s-navigation-item value="search">
    <s-icon slot="icon" name="search"></s-icon>
    <span slot="text">搜索</span>
  </s-navigation-item>
</s-navigation>
```

**JavaScript 交互**

```js
const nav = document.querySelector('s-navigation');
nav.addEventListener('change', () => console.log(nav.value));
nav.value = 'search';
```

---

## Page

### `<s-page>`

应用根容器，定义全局主题（色彩、阴影、动画等 CSS 变量），并支持明暗主题切换。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `theme` | `"light"` \| `"auto"` \| `"dark"` | `"auto"` | 主题模式 |

**暴露的方法**

| 方法 | 说明 |
|------|------|
| `toggle(theme, element?)` | 切换主题，返回 `Promise`。传入 `theme` 为目标主题，可选的 `element` 用于指定动画原点 |
| `get isDark()` | 获取当前是否为暗色主题（布尔值） |

**用法示例**

```html
<s-page theme="auto">
  <!-- 所有组件内容 -->
</s-page>
```

**JavaScript 交互**

```js
const page = document.querySelector('s-page');
page.toggle('dark'); // 切换至暗色主题
console.log(page.isDark); // true

// 以按钮为中心扩散切换主题
page.toggle('light', someButton);
```

---

## Pagination

### `<s-pagination>`

分页导航。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | `1` | 当前页码 |
| `total` | `number` | `20` | 总条目数 |
| `count` | `number` | `20` | 每页条目数（用于计算总页数） |
| `type` | `"standard"` \| `"outlined"` | `"standard"` | 样式变体 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 页码变化时触发 |

**用法示例**

```html
<s-pagination value="1" total="100" count="10"></s-pagination>
```

**JavaScript 交互**

```js
const pager = document.querySelector('s-pagination');
pager.value = 3; // 切换到第3页
pager.addEventListener('change', () => console.log(pager.value));
```

---

## Picker / PickerItem

### `<s-picker>`

下拉选择器（弹出菜单式）。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 当前选中项的值（对应 PickerItem 的 `value`） |
| `label` | `string` | `""` | 未选择时显示的占位文本 |
| `disabled` | `boolean` | `false` | 禁用 |

**暴露的成员**

| 成员 | 类型 | 说明 |
|------|------|------|
| `options` | `PickerItem[]` | 所有选项 |
| `selectedIndex` | `number` | 当前选中索引 |
| `show()` | `function` | 打开下拉列表 |
| `close()` | `function` | 关闭下拉列表 |
| `toggle()` | `function` | 切换打开/关闭 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 自定义触发器（默认显示字段样式） |
| (默认) | `<s-picker-item>` 列表 |

---

### `<s-picker-item>`

下拉选项。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `selected` | `boolean` | `false` | 是否选中 |
| `value` | `string` | `""` | 值 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标 |
| (默认) | 选项文本 |
| `end` | 后缀图标 |

**用法示例**

```html
<s-picker label="选择城市">
  <s-picker-item value="bj">北京</s-picker-item>
  <s-picker-item value="sh">上海</s-picker-item>
  <s-picker-item value="gz">广州</s-picker-item>
</s-picker>
```

**JavaScript 交互**

```js
const picker = document.querySelector('s-picker');
picker.addEventListener('change', () => console.log(picker.value));
picker.show();
```

---

## Popup

### `<s-popup>`

弹出层组件，相对于触发元素定位。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `align` | `"center"` \| `"left"` \| `"right"` | `"center"` | 水平对齐方式 |

**事件**

| 事件名 | 类型 | 说明 |
|--------|------|------|
| `show` | `CustomEvent` (可取消) | 显示前触发 |
| `showed` | `Event` | 显示后触发 |
| `closed` | `Event` | 关闭后触发 |

**暴露的方法**

| 方法 | 说明 |
|------|------|
| `show(target?)` | 显示弹出层。`target` 可以是 HTMLElement 或 `{ x, y, origin }` 坐标对象 |
| `close()` | 关闭 |
| `toggle(target?)` | 切换 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 点击触发展开的元素 |
| (默认) | 弹出内容 |

**用法示例**

```html
<s-popup align="left">
  <s-button slot="trigger">菜单</s-button>
  <s-menu>
    <s-menu-item>选项1</s-menu-item>
    <s-menu-item>选项2</s-menu-item>
  </s-menu>
</s-popup>
```

**JavaScript 交互**

```js
const popup = document.querySelector('s-popup');
popup.show(); // 以 trigger 定位
popup.show(someElement);
popup.show({ x: 200, y: 100, origin: 'left top' });
```

---

## PopupMenu / PopupMenuItem

### `<s-popup-menu>`

弹出菜单容器，通常配合 `<s-popup-menu-item>` 和 `<s-menu>` 使用。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `group` | `""` \| `"start"` \| `"end"` | `""` | 菜单分组样式（显示分隔线） |

**暴露的方法**

| 方法 | 说明 |
|------|------|
| `show()` | 显示菜单 |
| `close()` | 关闭 |
| `toggle()` | 切换 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 触发器 |
| (默认) | 菜单内容（`<s-popup-menu-item>` 或 `<s-menu>`） |

---

### `<s-popup-menu-item>`

弹出菜单项。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标 |
| (默认) | 文本 |
| `end` | 后缀图标 |

**事件**

点击后会在 `<s-popup-menu>` 内冒泡 `click` 事件，菜单自动关闭。

**用法示例**

```html
<s-popup-menu>
  <s-icon-button slot="trigger" name="more_vert"></s-icon-button>
  <s-popup-menu-item>编辑</s-popup-menu-item>
  <s-popup-menu-item>删除</s-popup-menu-item>
</s-popup-menu>
```

**JavaScript 交互**

```js
const menu = document.querySelector('s-popup-menu');
menu.show();
menu.addEventListener('click', e => console.log(e.target));
```

---

## RadioButton

### `<s-radio-button>`

单选框组件。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | `false` | 是否选中 |
| `value` | `string` | `""` | 值 |
| `name` | `string` | `""` | 单选框组名（同 name 的自动互斥） |
| `disabled` | `boolean` | `false` | 禁用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `unchecked` | 未选中时的图标 |
| `checked` | 选中时的图标 |
| (默认) | 标签文本 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 选中后触发 |

**用法示例**

```html
<s-radio-button name="choice" value="a">选项 A</s-radio-button>
<s-radio-button name="choice" value="b" checked>选项 B</s-radio-button>
```

---

## Rate

### `<s-rate>`

评分组件（星级评价）。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | `5` | 当前评分 |
| `max` | `number` | `10` | 最大分值 |
| `min` | `number` | `0` | 最小分值 |
| `step` | `number` | `1` | 每步增量 |
| `readOnly` | `boolean` | `false` | 只读模式（隐藏滑块输入） |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 值改变后触发 |
| `input` | 交互过程中持续触发 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `track` | 自定义未选中星标图标 |
| `indicator` | 自定义选中星标图标 |

**用法示例**

```html
<s-rate value="3.5" max="5" step="0.5" readonly></s-rate>
<s-rate></s-rate>
```

---

## Ripple

### `<s-ripple>`

水波纹效果。一般作为内部组件使用，也可单独包裹元素。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `centered` | `boolean` | `false` | 水波从中心开始 |
| `attached` | `boolean` | `false` | 将水波效果附加到父元素上（而非自身） |

**用法示例**

```html
<s-ripple>
  <div style="padding:20px;background:#eee;">点击我有水波</div>
</s-ripple>
```

---

## ScrollView

### `<s-scroll-view>`

可滚动容器，带有自定义滚动条样式。

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | 任意内容 |

**用法示例**

```html
<s-scroll-view style="height:200px;">
  <div style="height:600px;">长内容...</div>
</s-scroll-view>
```

---

## Search

### `<s-search>`

搜索输入框。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 输入值 |
| `placeholder` | `string` | `""` | 占位文本 |
| `maxLength` | `number` | `-1` | 最大输入长度 |
| `readOnly` | `boolean` | `false` | 只读 |
| `disabled` | `boolean` | `false` | 禁用 |

**暴露的成员**

| 成员 | 说明 |
|------|------|
| `native` | 原生 `<input>` 元素引用 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 值变化且失去焦点或清空时触发 |
| `input` | 输入时触发 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 替换默认搜索图标 |
| `end` | 替换默认清空按钮 |
| `dropdown` | 下拉建议区域（常用于放置列表） |

**用法示例**

```html
<s-search placeholder="搜索内容..." value="关键词"></s-search>

<!-- 带下拉建议 -->
<s-search>
  <s-menu slot="dropdown">
    <s-menu-item>建议1</s-menu-item>
    <s-menu-item>建议2</s-menu-item>
  </s-menu>
</s-search>
```

**JavaScript 交互**

```js
const search = document.querySelector('s-search');
search.addEventListener('input', () => {
  console.log('当前输入:', search.value);
});
search.native.focus();
```

---

## SegmentedButton / SegmentedButtonItem

### `<s-segmented-button>`

分段按钮组容器。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 当前选中项的值 |
| `mode` | `"auto"` \| `"fixed"` | `"auto"` | 分布模式（自动宽度或平分宽度） |

**暴露的成员**

| 成员 | 说明 |
|------|------|
| `options` | 所有 SegmentedButtonItem 数组 |
| `selectedIndex` | 当前选中索引 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | `<s-segmented-button-item>` 列表 |

---

### `<s-segmented-button-item>`

分段按钮项。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `selected` | `boolean` | `false` | 是否选中 |
| `value` | `string` | `""` | 值 |
| `selectable` | `boolean` | `true` | 是否可选中（设为 false 只作为展示） |
| `disabled` | `boolean` | `false` | 禁用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标 |
| (默认) | 文本 |
| `end` | 后缀图标 |

**用法示例**

```html
<s-segmented-button>
  <s-segmented-button-item value="day" selected>日</s-segmented-button-item>
  <s-segmented-button-item value="week">周</s-segmented-button-item>
  <s-segmented-button-item value="month">月</s-segmented-button-item>
</s-segmented-button>
```

**JavaScript 交互**

```js
const segment = document.querySelector('s-segmented-button');
segment.addEventListener('change', () => console.log(segment.value));
segment.value = 'week';
```

---

## Skeleton

### `<s-skeleton>`

骨架屏占位，用于加载中的占位效果。

无属性、无插槽，可直接使用。

**用法示例**

```html
<s-skeleton style="width:200px;"></s-skeleton>
<s-skeleton style="width:80px;height:80px;border-radius:50%;"></s-skeleton>
```

---

## Slider

### `<s-slider>`

滑块组件。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | `0` | 当前值 |
| `min` | `number` | `0` | 最小值 |
| `max` | `number` | `100` | 最大值 |
| `step` | `number` | `1` | 步长 |
| `labeled` | `boolean` | `false` | 是否显示当前值标签 |
| `disabled` | `boolean` | `false` | 禁用 |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 最终改变后触发 |
| `input` | 拖动过程中触发 |

**用法示例**

```html
<s-slider value="30" labeled></s-slider>
<s-slider min="0" max="50" step="5"></s-slider>
```

---

## Snackbar

### `<s-snackbar>`

Snackbar 消息条组件，用于短暂提示。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `"none"` \| `"info"` \| `"success"` \| `"warning"` \| `"error"` | `"none"` | 消息类型 |
| `align` | `"auto"` \| `"top"` \| `"bottom"` | `"auto"` | 垂直位置（`auto` 在触屏设备顶部，否则底部） |
| `duration` | `number` | `4000` | 自动关闭时长（毫秒），设为 0 则不会自动关闭 |

**事件**

| 事件名 | 类型 | 说明 |
|--------|------|------|
| `show` | `Event` | 显示时触发 |
| `showed` | `Event` | 显示动画完成后 |
| `close` | `Event` | 关闭时触发 |
| `closed` | `Event` | 关闭动画完成后 |

**暴露的方法**

| 方法 | 说明 |
|------|------|
| `show()` | 显示 Snackbar |
| `close()` | 关闭 Snackbar |

**静态方法**

`Snackbar.builder(options)` - 快速创建 Snackbar。`options` 支持：
- `root` : 父容器
- `text` : 提示文本
- `type` : 类型
- `align` : 位置
- `duration` : 持续时间
- `icon` : 图标（HTML 字符串或元素）
- `action` : 操作按钮（字符串文本 或 `{ text, click }`）

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 点击触发展示的按钮 |
| `icon` | 自定义图标 |
| (默认) | 文本内容 |
| `action` | 操作按钮 |

**用法示例**

```html
<s-snackbar id="snack">
  <s-button slot="trigger">显示提示</s-button>
  这是一条消息
  <s-button slot="action">撤销</s-button>
</s-snackbar>
```

**JavaScript 交互**

```js
// 编程式创建
Snackbar.builder({ text: '操作成功', type: 'success' });

// 控制已有实例
const snack = document.getElementById('snack');
snack.show();
```

---

## Switch

### `<s-switch>`

开关切换组件。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | `false` | 是否开启 |
| `disabled` | `boolean` | `false` | 是否禁用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `icon` | 开关内部的图标（默认无） |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 切换后触发 |

**用法示例**

```html
<s-switch checked></s-switch>
<s-switch disabled></s-switch>
```

**JavaScript 交互**

```js
const sw = document.querySelector('s-switch');
sw.addEventListener('change', () => console.log(sw.checked));
```

---

## Tab / TabItem

### `<s-tab>`

选项卡容器（标签栏）。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 当前选中的 TabItem 值 |
| `mode` | `"scrollable"` \| `"fixed"` | `"scrollable"` | 标签栏模式（滚动或平分） |

**暴露的成员**

| 成员 | 说明 |
|------|------|
| `options` | 所有 TabItem 数组 |
| `selectedIndex` | 当前选中索引 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| (默认) | `<s-tab-item>` 列表 |

---

### `<s-tab-item>`

选项卡项。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `selected` | `boolean` | `false` | 是否选中 |
| `value` | `string` | `""` | 值 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `icon` | 图标 |
| `text` | 文本标签 |
| `badge` | 徽章 |

**用法示例**

```html
<s-tab>
  <s-tab-item value="tab1" selected>
    <s-icon slot="icon" name="home"></s-icon>
    <span slot="text">首页</span>
  </s-tab-item>
  <s-tab-item value="tab2">
    <span slot="text">消息</span>
    <s-badge slot="badge">5</s-badge>
  </s-tab-item>
</s-tab>

<s-page> <!-- 结合页面内容切换 -->
  <div id="content-tab1">内容1</div>
  <div id="content-tab2" style="display:none">内容2</div>
</s-page>

<script>
  document.querySelector('s-tab').addEventListener('change', (e) => {
    const tab = e.currentTarget;
    document.getElementById('content-tab1').style.display = tab.value === 'tab1' ? '' : 'none';
    document.getElementById('content-tab2').style.display = tab.value === 'tab2' ? '' : 'none';
  });
</script>
```

---

## Table / Thead / Tbody / Tr / Th / Td

表格系列组件，通过 Web Components 实现原生 `<table>` 语义。

**标签与作用**

| 标签 | 作用 |
|------|------|
| `<s-table>` | 表格容器 |
| `<s-thead>` | 表头行组 |
| `<s-tbody>` | 表体行组 |
| `<s-tr>` | 表行 |
| `<s-th>` | 表头单元格 |
| `<s-td>` | 数据单元格 |

无特殊属性，按原生表格结构嵌套即可。

**用法示例**

```html
<s-table>
  <s-thead>
    <s-tr>
      <s-th>名称</s-th>
      <s-th>数量</s-th>
      <s-th>价格</s-th>
    </s-tr>
  </s-thead>
  <s-tbody>
    <s-tr>
      <s-td>商品A</s-td>
      <s-td>10</s-td>
      <s-td>¥99</s-td>
    </s-tr>
    <s-tr>
      <s-td>商品B</s-td>
      <s-td>5</s-td>
      <s-td>¥199</s-td>
    </s-tr>
  </s-tbody>
</s-table>
```

---

## TextField

### `<s-text-field>`

文本输入字段，功能丰富的输入组件。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | `""` | 输入值 |
| `label` | `string` | `""` | 标签文本 |
| `placeholder` | `string` | `""` | 占位文本 |
| `type` | `"text"` \| `"number"` \| `"password"` \| `"multiline"` | `"text"` | 输入类型 |
| `disabled` | `boolean` | `false` | 禁用 |
| `readOnly` | `boolean` | `false` | 只读 |
| `error` | `boolean` | `false` | 错误状态（红色边框） |
| `maxLength` | `number` | `-1` | 最大输入长度 |
| `countered` | `boolean` | `false` | 是否显示字符计数（仅 multiline 时默认显示） |
| `multiLine` | `boolean` | `false` | (已废弃) 使用 `type="multiline"` 代替 |

**暴露的成员**

| 成员 | 类型 | 说明 |
|------|------|------|
| `native` | `HTMLInputElement` 或 `HTMLTextAreaElement` | 原生输入元素引用 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `start` | 前导图标/按钮 |
| `end` | 后缀图标/按钮 |
| `text` | 辅助文本（显示在字段下方） |

**事件**

| 事件名 | 说明 |
|--------|------|
| `change` | 值改变时触发 |
| `input` | 输入过程中触发 |

**用法示例**

```html
<s-text-field label="用户名" placeholder="请输入用户名" value="张三"></s-text-field>

<s-text-field type="password" label="密码">
  <s-icon slot="start" name="lock"></s-icon>
</s-text-field>

<s-text-field type="multiline" label="备注" maxLength="200" countered></s-text-field>

<s-text-field type="number" value="5" step="1" min="0" max="10"></s-text-field>
```

**JavaScript 交互**

```js
const input = document.querySelector('s-text-field');
input.addEventListener('change', () => console.log(input.value));
input.error = true;
input.native.focus();
```

---

## Tooltip

### `<s-tooltip>`

提示气泡。

**属性**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `align` | `"top"` \| `"bottom"` \| `"left"` \| `"right"` | `"top"` | 提示位置 |
| `disabled` | `boolean` | `false` | 禁用提示 |

**插槽**

| 插槽名 | 说明 |
|--------|------|
| `trigger` | 触发元素 |
| (默认) | 提示内容文本或 HTML |

**用法示例**

```html
<s-tooltip align="bottom">
  <s-icon-button slot="trigger" name="info"></s-icon-button>
  这是提示信息
</s-tooltip>
```

**交互说明**

- 桌面端：鼠标悬停显示
- 移动端：长按触发

---

## 附录：CSS 自定义变量

所有颜色、阴影、运动曲线等均可通过 CSS 变量覆盖，默认变量在 `s-page` 元素上定义。主要变量列表如下（组件内部使用的均为这些变量）：

**颜色**
- `--s-color-primary`
- `--s-color-on-primary`
- `--s-color-primary-container`
- `--s-color-on-primary-container`
- `--s-color-secondary` / `--s-color-on-secondary` / `--s-color-secondary-container` / `--s-color-on-secondary-container`
- `--s-color-tertiary` / `--s-color-on-tertiary` / `--s-color-tertiary-container` / `--s-color-on-tertiary-container`
- `--s-color-error` / `--s-color-on-error` / `--s-color-error-container` / `--s-color-on-error-container`
- `--s-color-background` / `--s-color-on-background`
- `--s-color-surface` / `--s-color-on-surface`
- `--s-color-surface-variant` / `--s-color-on-surface-variant`
- `--s-color-outline` / `--s-color-outline-variant`
- `--s-color-surface-container` / `--s-color-surface-container-low` / `--s-color-surface-container-high` / `--s-color-surface-container-highest`
- `--s-color-success` / `--s-color-on-success` / `--s-color-success-container` / `--s-color-on-success-container`
- `--s-color-warning` / `--s-color-on-warning` / `--s-color-warning-container` / `--s-color-on-warning-container`
- `--s-color-scrim`

**暗色变量** (当 `<s-page dark>` 时自动切换)
- 对应暗色前缀 `--s-color-dark-*`

**阴影**
- `--s-elevation-level1` 至 `--s-elevation-level5`

**动画**
- `--s-motion-duration-short1` ~ `--s-motion-duration-extra-long4`
- `--s-motion-easing-standard` / `--s-motion-easing-standard-decelerate` / `--s-motion-easing-standard-accelerate`
- `--s-motion-easing-emphasized` / `--s-motion-easing-emphasized-decelerate` / `--s-motion-easing-emphasized-accelerate`

**组件级变量**
- 部分组件有自己的 CSS 变量，如 `--text-field-border-radius`, `--picker-border-radius`, `--search-outline-width` 等，详见各组件样式。

---

此文档涵盖了 Sober UI 库的所有公开组件及其完整用法。如需进一步定制样式，可通过覆盖上述 CSS 变量实现主题个性化。