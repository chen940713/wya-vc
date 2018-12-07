## [Demo Basic](https://wya-team.github.io/wya-vc/dist/m-notice-bar/basic.html)

## 功能
公告组件

## API

#### 属性

属性 | 说明 | 类型 | 默认值
---|---|---|---
text | 显示的文本 | `string` | -
type | 类型: `closeable` 点击按钮触发回调并隐藏组件, `link` 点击整个组件触发回调, `click` 点击按钮触发回调| `string`, 为空时右侧按钮不显示 | ''
showIcon | 是否显示图标 | `boolean` | false
renderIcon | 使用render自定义左侧图标组件 | `function` | 默认icon
renderBtn | 使用render自定义右侧按钮组件 | `function` | 默认按钮

#### 方法
属性 | 说明 | 类型 | 默认值
---|---|---|---
on-click | 三种点击类型触发的回调事件 | callback | -
icon-click | 非`link`类型下点击图标触发的回调事件 | callback | -
text-click | 非`link`类型下点击文本触发的回调事件 | callback | -

#### 自定义组件

```
renderIcon(h) {
	return h('div', {
		style: {
			color: '#000'
		}
	}, 'icon');
}
```

## 基础用法
```vue
<template>
	<div>
		<vc-notice-bar
			:text="text"
			type="click"
			show-icon
			:render-icon="renderIcon"
			@on-click="handleClick"
		/>
	</div>
</template>
<script>
import MNoticeBar from 'wya-vc';

export default {
	name: "vc-m-notice-bar-basic",
	components: {
		'vc-m-notice-bar': MNoticeBar,
	},
	data() {
		return {
			text: 'news news news',
		};
	},
	methods: {
		handleClick(){
			console.log('click');
		},
		renderIcon(h) {
			return h('div', {
				style: {
					color: '#000'
				}
			}, 'icon');
		}
	}
};
</script>
```
