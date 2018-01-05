# css-variables

css variables 变量 自定义属性 自定义属性级联变量:


动态性，可以在运行时更改
可以方便的从JS中读/写
可继承，可组合，同时具有作用域


定义变量：用这样的方式来声明一个变量：`--variable-name: variable-value;`（变量名是大小写敏感的）。变量的值可以是颜色、字符串、多个值的组合等。

使用变量：以这样的方式来使用一个变量: `some-css-value: var(--variable-name [, declaration-value]);`

全局变量：使用[:root](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)作用域来定义全局变量：

局部变量：如果想让某个变量只在部分元素/组件下可见，只需要在特定的元素下定义该变量。


变量可以和其他变量组合使用，`--variable-name: var(--another-variable-name);`

声明新变量的值不能直接由一个已定义的变量计算而来，但我们可以使用CSS calc()来代替:

```
.block {
    --block-font-size: 1rem;
}

.block__highlight {
    /* DOESN'T WORK */
    --block-highlight-font-size: var(--block-font-size)*1.5;
    font-size: var(--block-highlight-font-size);

    /* WORKS */
    font-size: calc(var(--block-font-size)*1.5);
}
```
对复杂的表达式要格外留心，它们很可能会影响到应用的性能。


使用CSS样式声明接口,可以在JS中方便的读/写自定义属性(getPropertyValue, setProperty):
```
// READ
const rootStyles = getComputedStyle(document.documentElement);
const varValue = rootStyles.getPropertyValue('--screen-category').trim();

// WRITE
document.documentElement.style.setProperty('--screen-category', value);
```

如果是为了调试， 可以通过伪类的content在页面上输出变量的值。

检测浏览器是否支持CSS自定义属性的方法

```css
@supports ( (--a: 0)) {
    /* supported */
}

@supports ( not (--a: 0)) {
    /* not supported */
}
```

```js
if (window.CSS && window.CSS.supports && window.CSS.supports('--a', 0)) {
    alert('CSS properties are supported');
} else {
    alert('CSS properties are NOT supported');
}
```

不支持supports，但是变量可能支持

[@supports](https://caniuse.com/#search=%40supports)

[variables](https://caniuse.com/#search=variables)

```js
function testCSSVariables() {
 var color = 'rgb(255, 198, 0)';
 var el = document.createElement('span');

 el.style.setProperty('--color', color);
 el.style.setProperty('background', 'var(--color)');
 document.body.appendChild(el);

 var styles = getComputedStyle(el);
 var doesSupport = styles.backgroundColor === color;
 document.body.removeChild(el);
 return doesSupport;
}
```


CSS和JS的语法级互动
动态性、可继承、可组合，同时拥有作用域
浏览器支持以及如何可靠地使用
可以和Sass变量一起使用
自定义变量拓展了开发者和web平台的能力，随之产生了一些有趣的用法和案例

预处理器的变量有一个主要的缺点，它们是静态的，不能在运行时更改。增加在运行时更改变量的能力不仅打开了诸如动态应用主题的大门，同时对响应式设计及补充将来的CSS特性的潜力具有重大影响。

CSS预处理器是很好的工具，但其变量是静态的，限定了语法作用域。另一方面，原生CSS变量是一种完全不同类型的变量：动态的，作用域是DOM。事实上，称它们为变量会令人迷惑。它们实际上是CSS属性，这为它们提供了一组完全不同的能力集，用来解决一系列完全不同的问题。

## 参考

[css变量](https://www.w3cplus.com/blog/tags/602.html)

[深入学习CSS自定义属性（CSS变量）2016-10-30](https://www.w3cplus.com/css3/css-properties-in-depth.html)

[我为什么对原生CSS变量感到兴奋 2017-02-20](https://www.w3cplus.com/css3/why-im-excited-about-native-css-variables.html)

[是时候开始使用CSS自定义属性 2017-04-22](https://www.w3cplus.com/css3/start-using-css-custom-properties.html)

[https://drafts.csswg.org/css-variables/](https://drafts.csswg.org/css-variables/)

[](https://webkit.org/blog/5989/css-variables-in-webkit/)

[](https://www.xanthir.com/blog/b4KT0)

[BEM](https://www.w3cplus.com/blog/tags/325.html)

[说说CSS中的@supports 2016-10-25](https://www.w3cplus.com/css3/supports-will-change-your-life.html)

[](https://justmarkup.com/log/2016/02/theme-switcher-using-css-custom-properties/)

[](https://hospodarets.com/css_apply_rule)

[](https://hospodarets.com/css_properties_in_depth)

[](http://kizu.ru/en/fun/conditions-for-css-variables/)

[](https://csswizardry.com/2016/10/pragmatic-practical-progressive-theming-with-custom-properties/)

[](https://googlechrome.github.io/samples/css-custom-properties/index.html)
