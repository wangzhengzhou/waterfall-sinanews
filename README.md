## 瀑布流效果新浪新闻网站
[预览地址](https://wangzhengzhou.github.io/waterfall-sinanews/)
## 懒加载原理
- 当一个页面有很多图片需要加载时，如果从一开始就加载则对性能有很大影响，导致用户只能在所有图片加载完成后才能使用。所以我们只是在用户浏览到当前图片时才加载它。其实现原理是判断当前的元素是否出现在视窗中，如果出现了就加载它；而判断当前元素是否在视窗中则是根据当前元素在页面的高度是否小于视窗的高度加上滚动的总高度，如果小于，则在视窗中，此时加载它，由此避免一次性大量发送请求，加载资源引起性能降低。同时，对于已经加载完成的元素可以在其上加上一个属性，当再次判断元素是否出现在视窗中时排除具有此属性的元素，避免重复判断，提高性能。
## 瀑布流原理
- 获取到需要布局的容器的宽度，用其除以元素的宽度取整得到一个数，将此数作为一个数组的元素个数，此数组中的每一个元素代表布局中的一列，每个元素的初始值都为0，其值代表的是布局中此列所有元素的高度和，每个元素的位置是插入到当前数组中值最小的那一列中，达到补足空缺的效果，每个元素使用绝对定位布局，其位置的左边距是其位置坐在列的下标乘以元素的宽度，其顶部的高度是当前列所有元素高度之和，即当前数组元素的值
## 实现原理
#### 此项目使用到懒加载和瀑布流布局两者，分为以下几步实现：
- 先写出一个DOM模版，设置CSS样式。使用绝对定位控制元素的位置
- 发送ajax请求获取数据
- 数据获取成功后拼装DOM结构
- DOM结构中的图片加载完成后对其位置进行设定
- 根据总宽度除以元素宽度确定存储元素位置顶部数据的数组内元素的个数
- 对数组初始化，每一项初始值设为0
- 对数组中的元素遍历，找到其中最小的元素作为下一个元素定位位置顶端的高度
- 定位位置左边的高度由其在数组中所在行的下标乘以元素的宽度确定
- 监听滚动区域出现滚动事件时判断此时未知是否到底，并留出一定冗余实现更佳的效果，判断到底后再次请求数据，拼装DOM，设置各元素位置
