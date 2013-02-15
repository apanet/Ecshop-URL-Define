注意事项：
1：如果使用了自定义重写，将不能同时启用“复杂重写”，只能启用“简单重写”
2：商品分类，文章分类，品牌定义URL不能使用中划线，即   -

首先进行数据库操作

执行以下SQL语句：

ALTER TABLE  `ecs_category` ADD  `define_url` VARCHAR( 255 ) NOT NULL , ADD INDEX (  `define_url` );
ALTER TABLE  `ecs_brand` ADD  `define_url` VARCHAR( 255 ) NOT NULL , ADD INDEX (  `define_url` );
ALTER TABLE  `ecs_article_cat` ADD  `define_url` VARCHAR( 255 ) NOT NULL , ADD INDEX (  `define_url` );
ALTER TABLE  `ecs_goods` ADD  `define_url` VARCHAR( 255 ) NOT NULL , ADD INDEX (  `define_url` );
ALTER TABLE  `ecs_article` ADD  `define_url` VARCHAR( 255 ) NOT NULL , ADD INDEX (  `define_url` );


1）、

需要修改到的文件

/category.php
/brand.php
/goods.php
/article_cat.php

/js/common.js

/includes/cls_template.php
/includes/lib_common.php

/admin/category.php
/admin/goods.php
/admin/brand.php
/admin/articlecat.php
/admin/templates/category_info.dwt
/admin/templates/brand_info.dwt
/admin/templates/articlecat_info.dwt
/admin/templates/goods_info.dwt
/admin/templates/article_info.dwt

/.htaccess


2）

修改方法：

用代码编辑软件（例如：editplus）打开我发给你的这些文件，
搜索 “ thunje#URLdf ” ，搜索到的位置，就是我做过修改的地方，

然后按照我修改的代码，修改你网站上的同名文件即可。
例如：打开 /category.php ，对照着修改你网站下的 /category.php

举例说明：

用代码编辑软件（例如editplus）打开  /category.php  文件
搜索   “ thunje#URLdf ”
能搜索到



/* 代码增加_start  By thunje#URLdf */
elseif(isset($_REQUEST['defurl']))
{
	$define_url=trim($_REQUEST['defurl']);
	$cat_id=$db->getOne("select cat_id from ". $ecs->table('category') ." where define_url='$define_url' limit 0,1");
	$cat_id=$cat_id ? $cat_id : 0;
}
/* 代码增加_end  By thunje#URLdf */


#注：插件原开发者：www.ecshop120.com



说明这段代码是 我新增加的，
你把这段代码增加到你网站同名文件的相同位置即可，要找准位置哦。。


恢复网站，去掉全站伪静态功能：
只要 恢复 根目录的.htaccess以及 includes/lib_common.php 就可以。