<template>
	<vc-notice-bar
		:text="text"
		:show-icon="true"
		:show-close="true"
		style="color: #f76a24; background-color: #fefcec;" />
</template>
<script>
import MNoticeBar from '../index';

export default {
	name: 'vc-notice-bar-basic',
	components: {
		'vc-notice-bar': MNoticeBar,
	},
	data() {
		return {
			// text: 'news news news news news news news news news news news.'
			text:
				'我的家在东北我的家在东北我的家在东北我的家在东北我的家在东北我的家在东北',
		};
	},
	computed: {},
	methods: {},
};
</script>
