
插件已发布到npm，执行以下命令就可以使用


vue插件移动框
 npm i dragablemodel -S（安装插件）

import dragablemodel from 'dragablemodel'

Vue.use(loading)

模板（组件）

<dragablemodel v-model='modal'>
<span slot="top"></span>
<div slot="main">
 
</div>
</dragablemodel>