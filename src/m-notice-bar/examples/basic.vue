<template>
	<vc-m-notice-bar
		:text="text"
		show-icon
		type="click"
		@on-click="handleClickBar"
		@icon-click="handleIconClick"
		@text-click="handleTextClick"
	/>
</template>
<script>
import MNoticeBar from '../index';

export default {
	name: 'vc-m-notice-bar-basic',
	components: {
		'vc-m-notice-bar': MNoticeBar,
	},
	data() {
		return {
			text: 'news news news news news news news news news news news.'
		};
	},
	methods: {
		handleClickBar() {
			console.log('click');
		},
		handleIconClick() {
			console.log('icon click');
		},
		handleTextClick() {
			console.log('text click');
		},
		renderIcon(h) {
			return h('div', {
				style: {
					color: 'red',
					fontSize: '20px'
				}
			}, 'icon');
		},
	},
};
</script>
