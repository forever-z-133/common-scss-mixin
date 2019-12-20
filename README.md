常见而公用的 scss 的 mixin 方法，且只有 mixin 方法，

## 1、如何使用

```
npm i -S common-scss-mixin
```

```scss
// xxx.scss
@import '~common-scss-mixin';

.someClass {
  @include pos-top(); /* 顶部定位 */
  @include flex-row(); /* flex 行且水平居中 */
  @include child-gap-right(); /* 子元素之间距离为 10px */
  @include border-bottom(); /* 底部毛细线 */
}
```

## 2、如何自定义

```scss
@function px($n) {
  @return $n * 1rem;
}
@import '~common-scss-mixin';
```

```scss
// 也有打包好的 css 可供使用，但类名会有所不同
@import 'common-scss-mixin/dist.min.css';
```

可配置项一览：
```scss
@function px($px) {}

$gap-xs: px(5);
$gap-sm: px(10);
$gap-md: px(15);
$gap-xl: px(30);
$row-gap: $gap-md;
$child-gap: $gap-xs;

$radius-md: px(4);
$radius-round: 1000px;
$radius-circle: 50%;

$border-width: px(1);
$border-color: #e8e8e8;
```

## 3、总览

```scss
@include border($color);
@include border-top($color);
@include border-left($color);
@include border-right($color);
@include border-bottom($color);
@include raduis($rdius);
@include radius-round();
@include radius-circle();

@include padding-row($gap);
@include padding-col($gap);
@include margin-row($gap);
@include margin-col($gap);
@include margin-center();
@include child-gap-right($gap);
@include child-gap-bottom($gap);

@include flex-row-normal();
@include flex-row($child);
@include flex-row-top();
@include flex-row-middle();
@include flex-row-bottom();
@include flex-row-stretch();
@include flex-row-left();
@include flex-row-center();
@include flex-row-right();
@include flex-row-wrap();

@include flex-col-normal();
@include flex-col($child);
@include flex-col-top();
@include flex-col-middle();
@include flex-col-bottom();
@include flex-col-stretch();
@include flex-col-left();
@include flex-col-center();
@include flex-col-right();

@include flex-center();

@include inblock-row();
@include float-row();
@include scroller($dir);
@include scroller-x();
@include scroller-y();

@include input-file();

@include cover();
@include fit-cover($fit);
@include pos-center();
@include pos-top();
@include pos-bottom();
@include pos-left();
@include pos-right();

@include text-overflow($line);
@include text-last-justify($height);

@include reset();
@include normal-list();
@include clearfix();
@include rect-box($width);
@include disabled();
@include ratio($ratio);
@include image-ratio($ratio, $fit);

px();
sin($angle);
cos($angle);
tan($angle);
```