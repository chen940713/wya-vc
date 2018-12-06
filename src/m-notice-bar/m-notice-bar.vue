<template>
	<div v-if="visible" class="vcm-notice-bar">
		<div v-if="showIcon" class="_icon">1</div>
		<div ref="notice-bar-text" class="_text">
			<div ref="notice-bar-content" class="_content">{{ text }}</div>
		</div>
		<div v-if="showClose" class="_btn" @click="handleClose()">xxxxx</div>
		<div v-if="showEnter" class="_btn">></div>
	</div>
</template>

<script>
export default {
	name: 'vcm-notice-bar',
	props: {
		text: {
			type: String,
			default: ''
		},
		showClose: {
			type: Boolean,
			default: false
		},
		showEnter: {
			type: Boolean,
			default: false
		},
		showIcon: {
			type: Boolean,
			default: false
		},
	},

	data() {
		return {
			visible: true
		};
	},
	mounted() {
		const el = this.$refs['notice-bar-content'];
		const wrap = this.$refs['notice-bar-text'];
		let width = el.scrollWidth;
		let wrapWidth = wrap.clientWidth;
		el.innerHTML = this.text + '&nbsp;&nbsp;&nbsp;&nbsp;' + this.text;
		let count = 0;
		let leave = 20;
		this.timer = setInterval(() => {
			count -= 10;
			if (count < width * -1 - leave) {
				el.style.transition = 'none';
				el.style.left = `${0}px`;
				count = 0;
			} else {
				el.style.transition = 'all .3s linear';
				el.style.left = `${count}px`;
			}
		}, 300); // 动画时间
	},
	destroyed() {
		this.timer && clearTimeout(this.timer);
	},
	methods: {
		handleClose(e) {
			this.visible = false;
			this.timer && clearTimeout(this.timer);
			this.$emit('close');
		},
		handleEnter() {

		}
	}
};
</script>

<style lang="scss" scoped>
.vcm-notice-bar{
	display: flex;
	._icon{
		margin-left: 20px;
	}
	._btn{
		padding-right: 10px;
	}
	._text{
		flex: 1;
		margin: 0 10px;
		overflow: hidden;
		position: relative;

		._content{
			white-space: nowrap;

			position: absolute;
			top: 0;
			left: 0;
		}
	}
}
</style>
