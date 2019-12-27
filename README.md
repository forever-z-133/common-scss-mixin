常见而公用的 scss 的 mixin 方法，且只有 mixin 方法，避免无端增加打包体积。

## 1、如何使用

```
npm i -S common-scss-mixin
```

### 使用 scss

```scss
// xxx.scss
@import '~common-scss-mixin';

.someClass {
  @include pos-top(); /* 顶部定位 */
  @include flex-row(); /* flex 行且水平居中 */
  @include padding-row(); /* 两边加上 15px 的内边距 */
  @include child-gap-right(); /* 子元素之间间隙为 10px */
  @include border-bottom(); /* 底部毛细线 */
}
```

### 使用 css

```scss
// 也有打包好的 css 可供使用，但类名会有所不同
// 如果喜欢本项目的话，可通过源码进一步尝试
@import 'common-scss-mixin/dist.min.css';
```
```html
<div class="post-top flex-row padding-row gap-right-5 border-bottom"></div>
```

### 使用单个 scss

```scss
// 如果担心编译太多 mixin 会影响性能，可分别引入
@import '~common-scss-mixin/src/border.scss';
@import '~common-scss-mixin/src/flex.scss';
@import '~common-scss-mixin/src/form.scss';
@import '~common-scss-mixin/src/gap.scss';
@import '~common-scss-mixin/src/layout.scss';
@import '~common-scss-mixin/src/others.scss';
@import '~common-scss-mixin/src/position.scss';
@import '~common-scss-mixin/src/text.scss';
@import '~common-scss-mixin/src/utils.scss';
@import '~common-scss-mixin/src/var.scss';

// 单个 css 则可以自己打包
@import '~common-scss-mixin/src/flex.scss';
@include flex-build();
```

### 全局使用 scss

不想每个地方都去 @import，可使用 sass-loader 配置,
让其加在编译前达到全局使用的效果，只管 @include 即可。

```js
// 以 vue-cli 的 vue.config.js 举例:
module.exports = {
  css: {
    loaderOptions: {
      sass: {
        // 当 sass-loader 版本低于 7.0 时需改为 data
        prependData: "@import 'common-scss-mixin';"
      }
    }
  }
}
```

## 2、如何自定义

```scss
@function px($n) {
  @return $n * 1rem;
}
@import '~common-scss-mixin';
```

可配置项一览：
```scss
@function px($n) { @return $n * 1px; }

$gap-xs: px(5);
$gap-sm: px(10);
$gap-md: px(15);
$gap-xl: px(30);
$row-gap: $gap-md;
$child-gap: $gap-sm;

$radius-md: px(4);
$radius-round: 1000px;
$radius-circle: 50%;

$border-width: 1PX;
$border-color: #e8e8e8;
```

## 3、总览

```scss
/* border.scss */
@include border($color);
@include border-top($color);
@include border-left($color);
@include border-right($color);
@include border-bottom($color);
@include raduis($rdius);
@include radius-round();
@include radius-circle();

/* gap.scss */
@include padding-row($gap);
@include padding-col($gap);
@include margin-row($gap);
@include margin-col($gap);
@include margin-center();
@include child-gap-right($gap);
@include child-gap-bottom($gap);

/* flex.scss */
@include flex-row-normal();
@include flex-row($child);
@include flex-row-top();
@include flex-row-middle();
@include flex-row-bottom();
@include flex-row-stretch();
@include flex-row-left();
@include flex-row-center();
@include flex-row-right();
@include flex-row-space(); // space-between 贴边
@include flex-row-wrap();

@include flex-col-normal();
@include flex-col($child);
@include flex-col-top();
@include flex-col-middle();
@include flex-col-bottom();
@include flex-col-space();
@include flex-col-left();
@include flex-col-center();
@include flex-col-right();

@include flex-center();

/* layout.scss */
@include inblock-row();
@include float-row();
@include scroller($dir);
@include scroller-x();
@include scroller-y();

/* form.scss */
@include input-file();

/* position.scss */
@include cover();
@include fit-cover($fit);
@include pos-center();
@include pos-top();
@include pos-bottom();
@include pos-left();
@include pos-right();

/* text.scss */
@include text-overflow($line);
@include text-last-justify($height);

/* others.scss */
@include reset();
@include normal-list();
@include clearfix();
@include rect-box($width);
@include disabled($grey);
@include ratio($ratio);
@include image-ratio($ratio, $fit);
@include seo-only();

/* utils.scss */
@mixin child-map() { $content }
sin($angle);
cos($angle);
tan($angle);
```