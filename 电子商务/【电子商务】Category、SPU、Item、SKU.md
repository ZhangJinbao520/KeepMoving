<!-- @title: 【电子商务】类目、SPU、Item、SKU -->
<!-- @date: 2021-11-01 13:39:35 -->
<!-- @author: Zhang Jinbao -->

[TOC]

## Category

类目是一个树状结构的系统，一般在系统内可分为 4~5 级，如：手机—>智能手机—>Apple 手机—>iPhone 13。

> 💬说明：从广义上来说，`类目`>`SPU`>`Item`>`SKU`。

<div align="center">
<img src="https://images.weserv.nl/?url=https://wx1.sinaimg.cn/large/8fa5dcfcgy1fz06l7bn09j20f00buacs.jpg" name="电商系统中的 SKU、SPU 数据库设计" />
</div>


## SPU

SPU（Standard Product Unit）是标准化产品单元，是商品信息聚合的最小单位，是一组可复用、易检索的标准化信息集合，该集合秒速了一个产品的特性。

> 💬说明</font>：SPU 是一“<font color="purple">款”商品。

- 信息聚合：具有有识别度的信息被用来作为不同 SPU 的区分点
- 易检索：通过`关键属性` +` 属性值`的聚合来实现易检索这个特性，哪些属性和属性值会被选为区分 SPU 的关键属性也是会随着场景变化而变化的
- 标准化的信息集合：一个抽象概念，如：Apple iPhone 13

SPU 也可以理解为是由“品牌+型号+关键属性”构成的，如：Apple iPhone 13  128G。

<div align="center">
<img src="https://pic2.zhimg.com/80/v2-eaf184b9bc4c76309a574ce114376476_1440w.jpg" name="SKU 层级关系" />
<div>



## Item

Item 更多的是指“单品”的概念；它即是一个抽象性概念，也是一个场景性概念，是在一定场景下讨论/交易的最小单元。

> 💬说明：淘宝叫 Item，京东叫 Product。

举个栗子🌰：

在华强北，一个单品可能是 Apple iPhone 13；但在苹果旗舰店，一个单品可能是 Apple iPhone 13  512G  粉红色。



## SKU

SKU 即库存进出计量的基本单元（最小单元），其单位可以是件、盒、托盘等；SKU 是商品的唯一标识，每个 SKU 都具有独立的条形码和库存管理。

> 💬说明</font>：SKU 是一“<font color="purple">件”商品。

也可以简单理解为 SKU 就是商品的具体规格：品牌、颜色、尺码等信息，如：“Apple iPhone 13  128G  粉红色“是一个 SKU，“Apple iPhone 13  256G  粉红色“是另外一个 SKU，“Apple iPhone 13  512G  粉红色“又是另外一个 SKU。

> 💬说明</font>：SKU 是一个具有场景性和相对性的概念。

举个栗子🌰：

SKU 是物理上不可分割的最小存货单元，但在使用时需要依据不同的业态和管理模型进行设定。

已知一箱香烟有 50 条、一条有 10 包、一包有 20 支，而在实际中需要根据不同的场景来设定 SKU，如：批发市场一般是按箱来卖的、大卖场一般是按条来卖的、零售店一般是按包来卖的、街边路摊可能是按支来卖的。

<div align="center">
<img src="https://pic2.zhimg.com/80/v2-50510fd3d60684e667464e14a560f0b3_1440w.jpg" name="SKU 分析" />
<div>