# hotelscore
酒店评分项目
## 开发工具: IDEA

## 开发环境: Tomcat7+JDK1.8+MySQL5.6

## 使用技术: html+css+Sevices+MyBatis+BootStrap+Spring+JSTL

## 需求

### 普通用户模块：

用户注册：用户名、密码、性别、出生日期、Email、手机、用户头像

浏览酒店信息：酒店名、酒店简介、酒店地址、酒店电话、酒店图片地址、酒店评分、酒店价格、酒店类型、设施/服务

- 可对酒店评分和评论，并在网站上对应的位置显示

用户个人管理中心：个人简介、个人电话、个人QQ、个人微信、个人生日、酒店评论、酒店打分

- 可对个人管理中心的信息进行修改

### 管理员模块：

管理员账号：用户名、密码

后台管理所有用户信息和酒店信息，对所有数据表进行操作

### 状态flag默认为0，1表示删除

## 1、用户注册表：user

|   列名   | 数据类型 | 长度 | 是否允许为空 | 默认值 |    说明    |
| :------: | :------: | :--: | :----------: | :----: | :--------: |
|  userid  |   int    |  16  |    不允许    |   1    | 主键，自增 |
| username | varchar  |  32  |    不允许    |        |   用户名   |
| password | varchar  |  16  |    不允许    |        |    密码    |
|   sex    | varchar  |  1   |    不允许    |   男   |    性别    |
| birthday |   date   |  8   |    不允许    |        |  出生日期  |
|  email   | varchar  |  32  |    不允许    |        |   Email    |
|  phone   | varchar  |  16  |    不允许    |        |    手机    |
|   pic    | varchar  |  32  |    不允许    |        |  用户头像  |
| regtime  | datetime |  0   |    不允许    |        |  注册时间  |
|   flag   |   int    |  1   |    不允许    |   0    |    状态    |

### date： YYYY-MM-DD

### datetime： YYYY-MM-DD HH:MM:SS 

### sql语句

```sql
CREATE TABLE user (
  userid int(16) NOT NULL AUTO_INCREMENT,
  username varchar(32) NOT NULL,
  password varchar(255) NOT NULL,
  sex varchar(1) NOT NULL DEFAULT '男',
  birthday date NOT NULL,
  email varchar(32) NOT NULL,
  phone varchar(16) NOT NULL,
  pic varchar(32) NOT NULL,
  regtime datetime DEFAULT NULL,
  flag int(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (userid)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



## 2、管理员信息表：admin


| 列名 | 数据类型 | 长度 | 是否允许为空 | 默认值 | 说明 |
| :----: | :--------: | :----: | :------------: | :------: | :----: |
| id | int | 16 | 不允许 | 1 | 主键，自增 |
| username | varchar | 32 | 不允许 |  | 用户名 |
| password | varchar | 16 | 不允许 |  | 密码 |

### sql语句

```sql
CREATE TABLE `admin` (
  `id` int(16) NOT NULL AUTO_INCREMENT,
  `username` varchar(32) NOT NULL,
  `password` varchar(16) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



## 3、酒店信息表：hotel


| 列名 | 数据类型 | 长度 | 是否允许为空 | 默认值 | 说明 |
| :----: | :--------: | :----: | :------------: | :------: | :----: |
| hotelid | int | 16 | 不允许 | 1 | 主键，自增 |
| hotelname | varchar | 32 | 不允许 |  | 酒店名 |
| introduction | varchar | 32 | 不允许 |  | 酒店简介 |
| address | varchar | 255 | 不允许 |  | 酒店地址 |
| phone | varchar | 16 | 不允许 |  | 酒店电话 |
| pic | varchar | 32 | 不允许 |  | 酒店简介图片地址 |
| score | double | 1 | 不允许 |  | 酒店评分 |
| price | double | 16 | 不允许 |  | 酒店价格 |
|     kind     | varchar  | 255  |     允许     |  其他  |     酒店类型     |
|   service    | varchar  | 255  |     允许     |   -    | 设施/服务 |
|     flag     | int | 1 | 不允许 | 0 | 状态 |

### 酒店评分根据所有的用户评分得出之后，计算其平均值

### sql语句

```sql
CREATE TABLE `hotel` (
  `hotelid` int(16) NOT NULL AUTO_INCREMENT,
  `hotelname` varchar(32) NOT NULL,
  `introduction` varchar(32) NOT NULL,
  `address` varchar(255) NOT NULL,
  `phone` varchar(16) NOT NULL,
  `pic` varchar(32) NOT NULL,
  `score` int(1) NOT NULL,
  `price` double(16,0) NOT NULL,
  `kind` varchar(255) DEFAULT NULL,
  `service` varchar(255) DEFAULT NULL,
  `flag` int(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`hotelid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



## 4、用户评论表：usercontent  


| 列名 | 数据类型 | 长度 | 是否允许为空 | 默认值 | 说明 |
| :----: | :--------: | :----: | :------------: | :------: | :----: |
| usercontentid | int | 16 | 不允许 | 1 | 主键，自增 |
| content | varchar | 255 | 不允许 |  | 评论内容 |
| time | date | 0 | 不允许 |  | 评价时间 |
|  hotelid   |   int    |  16  |    不允许    |        |   酒店id   |
|   userid   |   int    |  16  |    不允许    |        |   用户id   |
| flag | int | 1 | 不允许 | 0 | 状态 |

### date： YYYY-MM-DD



## 5、用户评分表：usergrade


| 列名 | 数据类型 | 长度 | 是否允许为空 | 默认值 | 说明 |
| :----: | :--------: | :----: | :------------: | :------: | :----: |
| usergradeid | int | 16 | 不允许 | 1 | 主键，自增 |
| grade | int | 1 | 允许 | | 酒店评分 |
| time | date | 0 | 不允许 | | 评价时间 |
| hotelid | int | 16 | 不允许 | | 酒店id |
| userid | int | 16 | 不允许 | | 用户id |
| flag | int | 1 | 不允许 | 0 | 状态 |

### 该表检测用户之前有无酒店评分，如果有，用户打分直接更改上一次打分的分数

### date： YYYY-MM-DD

### sql语句

```sql
CREATE TABLE `evaluate` (
  `evaluateid` int(11) NOT NULL AUTO_INCREMENT,
  `content` varchar(255) DEFAULT NULL,
  `level` int(1) NOT NULL,
  `time` date NOT NULL,
  `hotelid` int(16) NOT NULL,
  `userid` int(16) NOT NULL,
  `flag` int(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`evaluateid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



## 6、酒店图片表：hotelpicture


| 列名 | 数据类型 | 长度 | 是否允许为空 | 默认值 | 说明 |
| :----: | :--------: | :----: | :------------: | :------: | :----: |
| hotelpictureid | int | 16 | 不允许 | 1 | 主键，自增 |
|    hotelid     |   int    |  16  |    不允许    |        |   酒店id   |
| pic | varchar | 32 | 不允许 |  | 图片地址 |
| flag | int | 1 | 不允许 | 0 | 状态 |

### sql语句

```sql
CREATE TABLE `hotelpicture` (
  `hotelpictureid` int(16) NOT NULL AUTO_INCREMENT,
  `hotelid` int(16) NOT NULL,
  `pic` varchar(32) NOT NULL,
  `flag` int(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`hotelpictureid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



## 7、普通用户个人管理表（其他用户可访问）：personalhub


| 列名 | 数据类型 | 长度 | 是否允许为空 | 默认值 | 说明 |
| :----: | :--------: | :----: | :------------: | :------: | :----: |
| personalhubid | int | 16 | 不允许 | 1 | 主键，自增 |
| personalintroduction | varchar | 255 | 允许 | 暂无个人简介 | 个人简介 |
| phone | varchar | 16 | 允许 |  | 个人电话 |
| qq | int | 16 | 允许 |  | 个人QQ |
| WeChat | varchar | 32 | 允许 |  | 个人微信 |
| birthday | date | 0 | 允许 |  | 个人生日 |
| flag | int | 1 | 不允许 | 0 | 状态 |

### date： YYYY-MM-DD

### sql语句

```sql
CREATE TABLE `personalhub` (
  `personalhubid` int(16) NOT NULL AUTO_INCREMENT,
  `personalintroduction` varchar(255) DEFAULT NULL,
  `phone` varchar(16) DEFAULT NULL,
  `qq` int(16) DEFAULT NULL,
  `WeChat` varchar(32) DEFAULT NULL,
  `birthday` date DEFAULT NULL,
  `flag` int(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`personalhubid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```