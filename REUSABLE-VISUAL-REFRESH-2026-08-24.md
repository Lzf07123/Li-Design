# Li& 视觉刷新可复用规范（2026-08-24）

> 版本：V1.1 ｜ 日期：2026-11-07 ｜ 状态：可实例化（V1.1 回写卡片预烘焙玻璃调校：成片列表表面不叠加常驻 `backdrop-filter`，实时玻璃收敛到单一表面——见 §5、§10、§11；令牌与模板 CSS 未变）
> 用途：沉淀“液态玻璃卡片 / 瀑布流 / 卡片微交互 / 骨架屏 / 空状态 / 移动端二级菜单 / 右侧返回顶部”七组视觉模式的**完整实现契约**。
> 配套文件：`reusable-visual-refresh.template.css`（本规范的精确 CSS 实现）。
> 铁律：技术栈保持 Tailwind CSS 4；颜色/阴影/动效只进 tokens 文件；文案走项目 strings/brand 单点；公开站不新增用户输入组件；动效尊重 `prefers-reduced-motion`。

## 0. 一句话结论

所有页面使用统一留白与居中标题；卡片改为半透明磨砂玻璃并在悬浮时上浮加深投影；首页/项目列表使用 CSS 多列瀑布流且**未配置封面时不渲染默认占位图**；搜索索引异步加载时展示 shimmer 骨架屏；所有空列表使用 SVG 小图 + 引导文案；移动端把首页/关于/搜索外露在页眉、其余入口收进二级菜单；页面右下角常驻返回顶部按钮。

## 1. 组件清单与文件映射

| 模式 | 样式类 | 行为 | 复刻文件 |
| --- | --- | --- | --- |
| 液态玻璃令牌 | `--{{PROJECT_PREFIX}}-glass-*` | 半透明磨砂 + 折射高光 | `reusable-visual-refresh.template.css` |
| 留白 / 栅格 / 居中标题 | `.page-shell` `.section` `.section-title` `.page-title` | 静态布局 | 同 CSS |
| 玻璃卡片微交互 | `.project-card` `.post-card` `.journey-panel` | hover/focus 上浮 + 深投影 + 兄弟卡片弱化 | 同 CSS |
| 瀑布流 | `.masonry` | CSS columns 三→二→一列 | 同 CSS |
| 真实封面 | `.post-cover-link` `.post-cover` | 只有 `cover` 存在才渲染 | 卡片 partial |
| 移动端二级菜单 | `.mobile-nav-primary` `.mobile-menu` `.site-menu-*` | `<details>` + 原生 toggle 行为 | header partial + `nav-menu.js` |
| 右侧返回顶部 | `.back-to-top` | `href="#main"` 纯锚点 | baseof + CSS |
| 搜索骨架屏 | `.search-skeleton` `.search-skeleton-bar` | 异步索引加载占位 | search partial + inline JS |
| 空状态 | `.empty-state` `.empty-state-art` | SVG 小图 + 文案 + 可选动作 | `empty-state` partial |

## 2. 新增令牌（必须逐字一致）

浅色：

```css
:root {
  --{{PROJECT_PREFIX}}-glass-bg: rgba(255, 255, 255, 0.58);
  --{{PROJECT_PREFIX}}-glass-bg-strong: rgba(255, 255, 255, 0.78);
  --{{PROJECT_PREFIX}}-glass-border: rgba(255, 255, 255, 0.74);
  --{{PROJECT_PREFIX}}-glass-border-soft: rgba(225, 236, 232, 0.66);
  --{{PROJECT_PREFIX}}-glass-highlight: rgba(255, 255, 255, 0.82);
  --{{PROJECT_PREFIX}}-glass-shine: linear-gradient(135deg, rgba(255,255,255,.72), rgba(255,255,255,0) 46%);
  --{{PROJECT_PREFIX}}-glass-blur: 18px;
  --{{PROJECT_PREFIX}}-glass-saturate: 150%;
}
```

深色：

```css
.dark {
  --{{PROJECT_PREFIX}}-glass-bg: rgba(67, 73, 80, 0.56);
  --{{PROJECT_PREFIX}}-glass-bg-strong: rgba(67, 73, 80, 0.76);
  --{{PROJECT_PREFIX}}-glass-border: rgba(240, 242, 244, 0.18);
  --{{PROJECT_PREFIX}}-glass-border-soft: rgba(84, 92, 100, 0.68);
  --{{PROJECT_PREFIX}}-glass-highlight: rgba(240, 242, 244, 0.14);
  --{{PROJECT_PREFIX}}-glass-shine: linear-gradient(135deg, rgba(240,242,244,.16), rgba(240,242,244,0) 46%);
}
```

注意：`glass-blur` / `glass-saturate` 只写在 `:root`，深色继承同一值。

## 3. 留白 / 栅格 / 居中标题

| 参数 | 值 |
| --- | --- |
| 页面底部留白 | 96px |
| 首屏内容顶距 | 32px |
| 区块间距 | 72px |
| 卡片栅格 gap / margin | 24px |
| 卡片内边距 | 24px 28px |
| 栅格最小列宽 | 300px |
| 区块标题 | `text-align: center`，下装饰线 48×3px、圆角 2px、`margin: 10px auto 0` |
| 页面主标题 | `text-align: center` |

## 4. 瀑布流与封面规则（关键：不做默认占位图）

- 桌面 3 列：`column-width: 288px; column-gap: 24px;`
- 1024px：`column-width: 240px; column-gap: 20px;`
- 768px：2 列、`column-gap: 16px;`
- 640px：1 列。
- 卡片必须 `break-inside: avoid;`。
- 模板层：`{{ if cover }}` 才输出 `<a class="post-cover-link">…</a>`；**没有 cover 就没有图片元素**。
- 有 cover 时，图片用 `imageConfig` 读取宽高写入内联 `style="--cover-ratio: {{ width }} / {{ height }}"`；CSS 使用 `aspect-ratio: var(--cover-ratio, 16 / 9); height: auto; object-fit: cover; background: transparent;`。
- 不使用标题哈希生成抽象占位块；移除所有 `.card-visual` 类。

## 5. 玻璃卡片微交互

- 圆角 20px；边框 `glass-border-soft`；背景 `glass-shine + glass-bg`；`backdrop-filter: blur(18px) saturate(150%)`；内高光 `inset 0 1px 0 glass-highlight`。
- 不支持 `backdrop-filter` 时回退 `glass-bg-strong`。
- **成片列表表面改用预烘焙着色（V1.1 调校，实例验证：媒体库无限画布）**：`.project-card` / `.post-card` / `.journey-panel` 等成片出现的列表卡片，背景改为 `glass-shine + glass-bg-strong`，**不叠加常驻 `backdrop-filter`**。理由：卡片压在持续动画的氛围层上时，每卡常驻实时玻璃造成逐帧重采样，GPU/电量成本随卡片数量线性增长；`glass-bg-strong` 本就是无 backdrop 的回退底色，观感同源。卡片媒体元素不保留常驻 `will-change`，动画期间由浏览器自动提升合成层。
- **实时玻璃只保留在单一表面**：模态、媒体查看器、页眉、页脚、返回顶部等单实例表面继续用 `glass-bg` + `backdrop-filter: blur(18px) saturate(150%)`；这类表面同屏只有一两个，重采样成本恒定。
- 基础 hover：`translateY(-3px)` + `shadow-md`。
- 栅格/列表/瀑布流内聚焦态：`translateY(-5px) scale(1.006)` + `shadow-lg` + `border-color: primary`。
- 卡片顶部主色细线 hover/focus 展开（`scaleX(0→1)`）。
- 指针设备：兄弟卡片 `opacity: .55; scale(.985)`。
- 封面 hover 缩放 `1.03`。

## 6. 移动端二级菜单

### 6.1 菜单外露项
只保留 **首页、关于、搜索**；桌面导航中的 **文章、项目、历程、资源、友情链接** 折叠进 `<details>`。

### 6.2 DOM 契约

```html
<header class="site-header …">
  <a class="brand" href="{{ HOME }}">…</a>

  <!-- 桌面导航：所有入口 -->
  <nav class="site-nav ml-auto flex items-center gap-2" aria-label="主导航">
    <a class="site-nav-link" href="{{ HOME }}">首页</a>
    <a class="site-nav-link" href="{{ POSTS }}">文章</a>
    <a class="site-nav-link" href="{{ PROJECTS }}">项目</a>
    <a class="site-nav-link" href="{{ TIMELINE }}">历程</a>
    <a class="site-nav-link" href="{{ ABOUT }}">关于</a>
    <a class="site-nav-link" href="{{ RESOURCES }}">资源</a>
    <a class="site-nav-link" href="{{ FRIENDS }}">友情链接</a>
    <button class="nav-search-btn" data-open-search>搜索</button>
  </nav>

  <!-- 移动端外露项 -->
  <nav class="mobile-nav-primary" aria-label="主导航">
    <a class="mobile-nav-link" href="{{ HOME }}">首页</a>
    <a class="mobile-nav-link" href="{{ ABOUT }}">关于</a>
    <button class="mobile-nav-link mobile-nav-search" data-open-search>搜索</button>
  </nav>

  <!-- 移动端二级菜单 -->
  <div class="mobile-menu" data-mobile-menu>
    <details class="site-menu">
      <summary class="site-menu-trigger" aria-label="更多" aria-expanded="false">
        <span class="site-menu-icon site-menu-icon-open">☰</span>
        <span class="site-menu-icon site-menu-icon-close">✕</span>
        <span class="visually-hidden">更多</span>
      </summary>
      <nav class="site-menu-panel" aria-label="更多">
        <a class="site-menu-item" href="{{ POSTS }}">文章</a>
        <a class="site-menu-item" href="{{ PROJECTS }}">项目</a>
        <a class="site-menu-item" href="{{ TIMELINE }}">历程</a>
        <a class="site-menu-item" href="{{ RESOURCES }}">资源</a>
        <span class="site-menu-sep" aria-hidden="true"></span>
        <a class="site-menu-item" href="{{ FRIENDS }}">友情链接</a>
      </nav>
    </details>
  </div>
</header>
```

### 6.3 JS 行为契约
- 点外部：`details.removeAttribute("open")`。
- Escape：关闭并 `summary.focus()`。
- 菜单内链接点击：关闭。
- 搜索按钮点击：先关闭菜单再打开搜索。
- `aria-expanded` 随 `toggle` 事件同步。
- 触达尺寸恒为 44px；菜单面板 `min-width: 176px`、圆角 14px、右上角展开动画 150ms。
- ≤360px：隐藏品牌文字，仅保留 Logo，避免横向溢出。

## 7. 右侧常驻返回顶部

```html
<a class="back-to-top" href="#main" aria-label="返回顶部">
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
       stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
    <path d="M12 19V5"></path><path d="m5 12 7-7 7 7"></path>
  </svg>
</a>
```

- 固定右下角：桌面 `right:20px; bottom:24px`，移动 `right:14px; bottom:16px`。
- 44×44、圆角 14px、玻璃背景、`href="#main"` 纯锚点；不引入 JS。
- `html { scroll-behavior: smooth; }`；`prefers-reduced-motion` 时 `auto`。
- 打印隐藏；`z-index:55`。

## 8. 搜索骨架屏

DOM：

```html
<div id="search-modal-skeleton" class="search-skeleton" hidden aria-hidden="true">
  <div class="search-skeleton-item"><span class="search-skeleton-bar"></span><span class="search-skeleton-bar"></span></div>
  <div class="search-skeleton-item"><span class="search-skeleton-bar"></span><span class="search-skeleton-bar"></span></div>
  <div class="search-skeleton-item"><span class="search-skeleton-bar"></span><span class="search-skeleton-bar"></span></div>
</div>
```

状态机：
- 输入非空且索引未就绪：显示 skeleton，`status` 文案 = “正在加载搜索索引…”。
- 索引返回后：隐藏 skeleton 并立即渲染结果。
- 索引失败：隐藏 skeleton，显示“搜索索引加载失败，请稍后重试”。
- shimmer 周期 1.35s，`background-position` 120% → -20%。

## 9. 空状态

```html
<div class="empty-state">
  <div class="empty-state-art" aria-hidden="true">[42×42 内联 SVG 图标]</div>
  <p class="empty-state-text">暂无内容引导文案</p>
  <a class="empty-state-action" href="{{ HOME }}">返回首页</a>
</div>
```

- 容器 padding 48px 24px、圆角 22px、玻璃背景。
- 图标盒 84×84、圆角 28px、`primary-soft` 底、`primary` 图标色。
- 覆盖：文章 / 项目 / 时间线 / 标签 / 归档 / 友情链接空列表。

## 10. 断点与验收矩阵

| 视口 | 期望 |
| --- | --- |
| 320px | 品牌文字隐藏、只留 Logo；首页/关于/搜索 + 菜单；`document.documentElement.scrollWidth == innerWidth` |
| 390px | 同上，无横向溢出 |
| 768px | 移动端布局 |
| 769px | 桌面导航显示，`.mobile-nav-primary` / `.mobile-menu` 隐藏 |
| 1440px | 桌面导航显示，友情链接在“资源”之后 |

程序化验收（Chrome DevTools Protocol 实测值）：
- 390px：`.site-nav { display:none }`、`.mobile-nav-primary { display:flex }`、`.mobile-menu { display:block }`。
- 769px：`.site-nav { display:flex }`、`.mobile-nav-primary { display:none }`、`.mobile-menu { display:none }`。
- 悬浮卡片 computed transform：`matrix(1.006, 0, 0, 1.006, 0, -5)`。
- 成片卡片 computed backdrop-filter：`none`（预烘焙 `glass-bg-strong` 着色，V1.1）；模态 / 查看器 / 页眉 / 页脚 / 返回顶部等单一表面：`blur(18px) saturate(1.5)`。
- 搜索骨架屏在延迟 1200ms 时可见，返回后隐藏且结果列表出现。

## 11. 常见坑

1. **不要把响应式覆盖写进 `@layer components`**：`.site-nav { display:none }` 若在 components 层，会被 utilities 层的 `.flex` 覆盖。必须放在无层样式区（本模板 CSS 即无层样式）。
2. 不要为未配图内容生成默认渐变占位块。
3. 封面比例必须由 `imageConfig` 提供；缺失时使用 `16 / 9` 兜底。
4. 玻璃卡片文本仍需满足 AA：深色 rgba 软底只用于装饰，承载文本的玻璃层必须使用 `glass-bg-strong` 或可读前景。
5. 每个新增 animation 必须有 `@keyframes`；降级动效统一收敛为 `0.01ms` 单次。
6. **成片卡片不要每卡常驻 `backdrop-filter`（V1.1 性能坑）**：瀑布流/画布这类几十张卡同屏的表面，实时玻璃的逐帧重采样成本随卡数线性增长（压在持续动画氛围层上时最明显）；一律用 `glass-shine + glass-bg-strong` 预烘焙着色，实时玻璃只留给模态/查看器/页眉页脚/返回顶部等单一表面。
