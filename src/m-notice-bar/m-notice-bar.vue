<template>
	<div
		v-if="visible"
		class="vcm-notice-bar"
		@click="type === 'link' ? handleClick('link') : ''"
	>
		<div
			v-if="showIcon"
			class="_icon"
			@click="type !== 'link' ? handleIconClick() : ''"
		>
			<vc-customer-row :render="renderIcon"/>
		</div>

		<div
			class="_marquee-wrap"
			@click="type !== 'link' ? handleTextClick() : ''"
		>
			<marquee
				class="_marquee"
				align="middle"
				behavior="scroll"
				scrollamount="3"
			>{{ text }}</marquee>
		</div>

		<div
			v-if="type === 'closeable'"
			class="_btn"
			@click="handleClick('closeable')"
		>
			<vc-customer-row
				:render="renderBtn"
				type="closeable"
			/>
		</div>

		<div
			v-if="showBtn"
			class="_btn"
			@click="type === 'click' ? handleClick('click') : ''"
		>
			<vc-customer-row
				:render="renderBtn"
				type="link"
			/>
		</div>
	</div>
</template>

<script>
import CreateCustomer from '../create-customer/index';

const CustomerRow = CreateCustomer({
	type: String,
});

export default {
	name: 'vcm-notice-bar',
	components: {
		'vc-customer-row': CustomerRow,
	},
	props: {
		text: {
			type: String,
			default: '',
		},
		type: {
			type: String,
			default: '',
			validator(v) {
				// 必须匹配下列字符串中的一个
				return ['', 'closeable', 'link', 'click'].indexOf(v) !== -1;
			},
		},
		showIcon: {
			type: Boolean,
			default: false,
		},
		renderIcon: {
			type: Function,
			default(h) {
				return h('img', {
					attrs: {
						src: require('./svg/gg.svg'),
					},
				});
			},
		},
		renderBtn: {
			type: Function,
			default(h, { type }) {
				let close = h('img', {
					attrs: {
						src: require('./svg/close.svg'),
					},
				});
				let link = h('img', {
					attrs: {
						src: require('./svg/right.svg'),
					},
				});
				let dom = type === 'link' ? link : close;
				return dom;
			},
		},
	},
	data() {
		return {
			visible: true,
		};
	},
	computed: {
		showBtn() {
			return /^link|click$/.test(this.type);
		},
	},
	methods: {
		handleClick(action) {
			if (action === 'closeable') {
				this.visible = false;
			}
			this.$emit('on-click');
		},
		handleIconClick() {
			this.$emit('icon-click');
		},
		handleTextClick() {
			this.$emit('text-click');
		},
	},
};
</script>

<style lang="scss" scoped>
.vcm-notice-bar {
	display: flex;
	color: #f76a24;
	background-color: #fefcec;
	padding: 5px 0;
	._icon {
		margin-left: 10px;
		display: flex;
		justify-content: center;
		align-items: center;
		img {
			height: 15px;
		}
	}
	._btn {
		margin-right: 10px;
		display: flex;
		justify-content: center;
		align-items: center;
		img {
			height: 15px;
		}
	}
	._marquee-wrap {
		display: flex;
		justify-content: center;
		align-items: center;
		._marquee {
			margin: 0 5px;
		}
	}
}
</style>
