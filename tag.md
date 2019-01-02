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

tag的内部实现。

## Tag