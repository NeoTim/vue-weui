<style lang="less">

@import "./style/base/fn";
@weuiDialogBackgroudColor: #FAFAFC;
@weuiDialogLineColor: #D5D5D6;
@weuiDialogLinkColor: #3CC51F;
.weui_dialog {
    position: fixed;
    z-index: 13;
    width: 85%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: @weuiDialogBackgroudColor;
    text-align: center;
    border-radius: 3px;
    .weui_dialog_confirm & {
        .weui_dialog_hd {
            text-align: left;
            padding: 1.2em 20px .5em;
        }
        .weui_dialog_bd {
            text-align: left;
        }
    }
}

.weui_dialog_hd {
    padding: 1.2em 0 .5em;
}

.weui_dialog_title {
    font-weight: 400;
    font-size: 17px;
}

.weui_dialog_bd {
    padding: 0 20px;
    font-size: 15px;
    color: @globalTextColor;
}

.weui_dialog_ft {
    position: relative;
    line-height: 42px;
    margin-top: 20px;
    font-size: 17px;
    a {
        display: block;
        color: @weuiDialogLinkColor;
        text-decoration: none;
        .setTapColor;
        &:active,
        &:hover {
            text-decoration: none;
        }
    }
    &:after {
        content: " ";
        .setLine(@weuiDialogLineColor);
    }
    .weui_dialog_confirm & {
        a {
            position: relative;
            float: left;
            width: 50%;
            &:after {
                content: " ";
                .setLine(@weuiDialogLineColor, V);
            }
            &:first-child {
                &:after {
                    display: none;
                }
            }
            &:last-child {
                float: none;
                width: auto;
                overflow: hidden;
                *zoom: 1;
            }
        }
    }
}

.weui_btn_dialog {
    &.default {
        color: #353535;
    }
    &.primary {
        color: #0BB20C;
    }
}

@media screen and (min-width: 1024px) {
    .weui_dialog {
        width: 35%;
    }
}

</style>

<template>

<div :class="'weui_dialog_' + type" v-show="show">
    <div class="weui_mask"></div>
    <div class="weui_dialog">
        <div class="weui_dialog_hd">
            <strong class="weui_dialog_title">{{title}}</strong>
        </div>
        <div class="weui_dialog_bd">
            <slot>请注意，这里可以自定义(支持html)</slot>
        </div>
        <div class="weui_dialog_ft">
            <a href="javascript:;" class="weui_btn_dialog default" v-if="type === 'confirm'" @click="dispatch($event,  'on-' + type + '-cancel')">{{cancelBtn}}</a>
            <a href="javascript:;" class="weui_btn_dialog primary" @click="dispatch($event, 'on-' + type + '-confirm')">{{confirmBtn}}</a>
        </div>
    </div>
</div>

</template>

<script>

export default {
    name: 'Dialog',
    props: {
        //类型：alert,confirm
        type: {
            type: String,
            required: false,
            default: 'alert'
        },
        //标题
        title: {
            type: String,
            required: false,
            default: '温馨提示'
        },
        show: {
            type: Boolean,
            required: true,
            default: true
        },
        cancelBtn: {
            type: String,
            required: false,
            default: '取消'
        },
        confirmBtn: {
            type: String,
            required: false,
            default: '确定'
        }
    },
    methods: {
        // cancel() {
        //     this.show = false;
        // },
        // confirm() {
        //     this.show = false;
        // }，
        dispatch(event, eventStr) {
            this.$dispatch(eventStr);
            // this.show = false;
        }
    }
}

</script>
