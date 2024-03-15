---
title: DOTween使用记录
tags: 
    - 编程
    - unity
categories: 学习笔记
date: 2022-12-15 10:59:38
---
## 将DOTween导入unity项目
1. 从官方网站下载DOTween [DOTween](http://dotween.demigiant.com/download.php)
1. 

>[官方文档](http://dotween.demigiant.com/documentation.php)
## 基本结构

    //引用
    using DG.Tweening;
    //声明一个DOTween对象
    private Tween TweenObj;
    //声明一个动画队列
    private Sequence SequenceObj = DoTween.Sequence;

## Sequence


## 回调函数
|函数名|作用|
|---|---|
|OnComplete|指结束动作后触发|
|OnStepComplete|完成单个循环后触发|
|OnKill|是指所有运动结束时，才触发。|
|OnPlay|每次从暂停状态恢复播放时触发|
|OnPause|当状态从播放变为暂停时触发|
|OnStart|开始时调用|
|OnUpdate|每一帧调用|
|OnRewind|播放时到达起始位置时将触发|


## DOTween常实现的效果
- 基本的图形变化
    - 放大，缩小，位移，旋转，旋转，翻转（对RectTransform的控制）
    - 色彩变化，透明度变化（对Image的控制）
    - 轨迹移动
    - 快进慢放效果


## 播放速率曲线（缓动函数）
>https://www.cnblogs.com/Fallever/p/8871456.html

{%  image
    url="/assets/images/post/post44-1.png"
    title="常见的缓动函数"
%}
>来源 (https://easings.net/zh-cn)
DOTween缓动函数枚举

    public enum Ease
        {
            Unset = 0,
            Linear = 1,
            InSine = 2,
            OutSine = 3,
            InOutSine = 4,
            InQuad = 5,
            OutQuad = 6,
            InOutQuad = 7,
            InCubic = 8,
            OutCubic = 9,
            InOutCubic = 10,
            InQuart = 11,
            OutQuart = 12,
            InOutQuart = 13,
            InQuint = 14,
            OutQuint = 15,
            InOutQuint = 16,
            InExpo = 17,
            OutExpo = 18,
            InOutExpo = 19,
            InCirc = 20,
            OutCirc = 21,
            InOutCirc = 22,
            InElastic = 23,
            OutElastic = 24,
            InOutElastic = 25,
            InBack = 26,
            OutBack = 27,
            InOutBack = 28,
            InBounce = 29,
            OutBounce = 30,
            InOutBounce = 31,
            Flash = 32,
            InFlash = 33,
            OutFlash = 34,
            InOutFlash = 35,
            //
            // 摘要:
            //     Don't assign this! It's assigned automatically when creating 0 duration tweens
            INTERNAL_Zero = 36,
            //
            // 摘要:
            //     Don't assign this! It's assigned automatically when setting the ease to an AnimationCurve
            //     or to a custom ease function
            INTERNAL_Custom = 37
        }

## 可视化组件DOTweenAnimation组件






