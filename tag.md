# tag源码解读

tag实现了进行标记和分类的小标签。主要包括两个组件Tag和CheckableTag。

# CheckableTag

可以选中的tag。

## 依赖

classnames: 用于合并class

## 接口

```ts
export interface CheckableTagProps {
  prefixCls?: string; // class前缀，默认ant-tag
  className?: string; // 自定义class
  checked: boolean; // 选中状态
  onChange?: (checked: boolean) => void; // 点击标签回调
}
```

## class

利用className和合并prefixCls、className、checkable及根据checked增加checkable-checked。

删除props中的onChange，只有在onClick触发onChange，防止组件改变触发onChange。

返回一个div实现CheckableTag，使用className控制样式，handleClick控制是否选中。


# Tag

## 依赖

rc-animate: 实现react动画，后面会进一步学习rc-component

omit.js: 根据指定的key，删除map中的元素

react-lifecycles-compat: 用于兼容新旧版本的react生命周期,antd中已经改为新版的生命周期

icon: icon组件

_util/wave: 实现波浪的点击样式

## 接口

```ts
export interface TagProps extends React.HTMLAttributes<HTMLDivElement> {
  prefixCls?: string;
  className?: string;
  color?: string; // 标签色
  closable?: boolean; // 是否可以关闭
  visible?: boolean; // 是否显示标签
  onClose?: Function; // 关闭时回调
  afterClose?: Function; // 关闭动画完成后回调
  style?: React.CSSProperties; // 样式
}
```

## InnerTag

tag的内部实现。参数由InnterTagProps规定。

使用omit移除props中的部分属性，传给InnerTag。

## Tag

getDerivedStateFromProps: 根据props更新state，当传入的props中有visible，更新state中的visible。

setVisible: 点击关闭Tag触发的事件，当props指定onClose则调用onClose。下一步使用defaultPrevented判断onClose中是否调用过preventDefault阻止默认事件，如果调用过则直接返回。下一步检验props是否有visible，即外部是否控制Tag显示，如果没控制，则设置state中的visible隐藏Tag。

animationEnd: Animate组件动画执行结束时的回调，即Tag关闭后，如果props有传入afterClose，则调用。

isPresetColor: 使用正则判断判断props中的color是否为预置color。-inverse就是单纯可匹配的字符串后缀！

getTagStyle: 根据color控制Tag的背景色，当color不是预置颜色时，则直接将背景色设置为color。

getTagClassName: 获取Tag的class。当color为预置时，则设置对应的class。否则设置has-color这个class。最后根据visible设置hidden这个class。

renderCloseIcon: 渲染关闭Icon。

render: Tag渲染。外层包裹Wave组件实现点击的波纹效果。然后Animate包裹实现动画效果以及关闭后的回调。最后内部展示InnerTag组件，渲染出Tag，Tag内部展示children和关闭Icon。

