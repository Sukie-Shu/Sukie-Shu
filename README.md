/*
导航高级数据传输
源服务器 ： 本地Mysql5.7
源服务器类型 ： MySQL
源服务器版本 ： 50719
来源 主机 ： 本地主机：3306
源架构 ： e5
目标服务器类型 ： MySQL
目标服务器版本：50719
文件编码 ： 65001
日期： 04/02/2021 08：24：47
*/

设置名称 utf8mb4;
设置FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
--github 的表结构
-- ----------------------------
如果存在“github”，则删除表;
CREATE TABLE 'github`  (
  'id' int（11） not null AUTO_INCREMENT，
  'user_id' int（255） NULL DEFAULT NULL COMMENT 'Userid'，
  'access_token' varchar（255） 字符集 utf8mb4 整理 utf8mb4_general_ci 空默认空，
  'login' varchar（255） 字符集 utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '登录名'，
  'name' varchar（255） CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT 'github的用户名'，
  'avatar_url' varchar（255） 字符集 utf8mb4 整理 utf8mb4_general_ci NULL 默认 NULL 注释 '头像url'，
  'github_id' int（11） NULL DEFAULT NULL COMMENT 'ID'，
  使用 BTREE 的主键 （'id'）
） 引擎 = MyISAM AUTO_INCREMENT = 7480 字符集 = utf8mb4 COLLATE = utf8mb4_general_ci ROW_FORMAT = 动态;

-- ----------------------------
--展望表结构
-- ----------------------------
如果存在“展望”，请删除表;
创建表格 '展望`  (
  'id' int（11） not null AUTO_INCREMENT，
  'github_id' int（255） NULL DEFAULT NULL COMMENT 'Userid'，
  'id_token' varchar（2048） 字符集 utf8mb4 整理 utf8mb4_general_ci 空默认值 NULL，
  'client_id' varchar（255） 字符集 utf8mb4 整理 utf8mb4_general_ci 空默认空，
  'client_secret' varchar（255） 字符集 utf8mb4 整理 utf8mb4_general_ci 空默认空，
  'refresh_token' varchar（4096） 字符集 utf8mb4 整理utf8mb4_general_ci NULL 默认 NULL 注释 '刷新令牌'，
  'access_token' varchar（8196） 字符集 utf8mb4 整理utf8mb4_general_ci NULL DEFAULT NULL，
  'cron_time' int（11） NOT NULL DEFAULT 3600，
  'cron_time_random_start' int（11） NOT NULL DEFAULT 3600，
  “cron_time_random_end” int（11） NOT NULL DEFAULT 7200，
  'name' varchar（30） 字符集 utf8mb4 整理utf8mb4_general_ci NOT NULL COMMENT '名称'，
  'describes' varchar（255） CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL COMMENT '描述'，
  'step' int（1） NOT NULL DEFAULT 0 COMMENT 'Steps'，
  'status' int（1） NOT NULL DEFAULT 1 COMMENT '状态： 1、等待配置 2、暂停 3、运行中 4、封禁 5、已停止（由于调用错误导致的停止） 6、等待授权 7、授权失败 8 、配置时间'，
  'next_time' int（11） NOT NULL DEFAULT 0 COMMENT '下次调用时间'，
  使用 BTREE 的主键 （'id'）
） 引擎 = MyISAM AUTO_INCREMENT = 8002 字符集 = utf8mb4 COLLATE = utf8mb4_general_ci ROW_FORMAT = 动态;

-- ----------------------------
--outlook_log的表结构
-- ----------------------------
如果存在“outlook_log”，请删除表;
创建表outlook_log`  (
  'id' int（11） not null AUTO_INCREMENT，
  'github_id' int（11） NOT NULL COMMENT 'github_id'，
  'call_time' int（11） NULL DEFAULT NULL COMMENT '调用时间'，
  'result' int（1） NULL DEFAULT NULL COMMENT '调用结果'，
  'msg' varchar（255） 字符集 utf8mb4 整理 utf8mb4_bin NULL DEFAULT NULL COMMENT '如果有错误原因则记录'，
  'original_msg' varchar（4096） 字符集 utf8mb4 整理 utf8mb4_bin NULL DEFAULT NULL COMMENT '原始错误消息'，
  'outlook_id' int（11） NOT NULL COMMENT 'outlook_id'，
  主键 （'id'） 使用 BTREE，
使用 BTREE 索引 “github_id”（“github_id”）
） 引擎 = MyISAM AUTO_INCREMENT = 8 字符集 = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = 动态;

-- ----------------------------
--权限的表结构
-- ----------------------------
如果存在“权限”，请删除表;
创建表'权限`  (
  'id' int（11） not null AUTO_INCREMENT，
  `permission` varchar(30) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '所拥有的权限',
  PRIMARY KEY (`id`) USING BTREE
） 引擎 = MyISAM AUTO_INCREMENT = 4 字符集 = utf8mb4 COLLATE = utf8mb4_general_ci ROW_FORMAT = 动态;

-- ----------------------------
--角色的表结构
-- ----------------------------
如果存在“角色”，则删除表;
创建表'角色`  (
  'id' int（11） not null AUTO_INCREMENT，
  'rolename' varchar（30） CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '角色名称'，
  'permission' varchar（2） 字符集 utf8mb4 整理 utf8mb4_general_ci NULL DEFAULT '0' COMMENT '权限 ID'，
  使用 BTREE 的主键 （'id'）
） 引擎 = MyISAM AUTO_INCREMENT = 2 字符集 = utf8mb4 COLLATE = utf8mb4_general_ci ROW_FORMAT = 动态;

-- ----------------------------
--用户的表结构
-- ----------------------------
如果存在“用户”，则删除表;
创建表'用户`  (
  'id' int（11） not null AUTO_INCREMENT，
  'name' varchar（255） 字符集 utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL，
  'passwd' varchar（64） CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '密码使用sha512'，
  'role' char（2） 字符集 utf8mb4 整理 utf8mb4_general_ci 空 默认空注释 '角色 ID'，
  'email' varchar（100） 字符集 utf8mb4 整理 utf8mb4_general_ci NOT NULL COMMENT '邮箱'，
  'status' varchar（2） 字符集 utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '账户状态，1、启用 0、禁用'，
  主键（“id”、“电子邮件”）使用 BTREE，
索引 'id'（'id'） USING BTREE，
索引“电子邮件”（“电子邮件”）使用BTREE
） 引擎 = MyISAM AUTO_INCREMENT = 5 字符集 = utf8mb4 COLLATE = utf8mb4_general_ci ROW_FORMAT = 动态;

设置FOREIGN_KEY_CHECKS = 1;
