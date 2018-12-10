# 机场数据

## 来源信息


首页: http://ourairports.com/

下载来源: http://ourairports.com/data/

数据条数: **54,822** 

最后更新时间: 2018-12-10

### 2018-12-10 20:00 csv文件快照

[ourairports.com_data_20181210.zip](ourairports.com_data_20181210.zip)



### 文件说明

> - [airports.csv](http://ourairports.com/data/airports.csv) (8,293,754 bytes, last modified Dec 10, 2018)
>
>   Large file, containing information on all airports on this site.
>
> - [airport-frequencies.csv](http://ourairports.com/data/airport-frequencies.csv) (1,207,279 bytes, last modified Dec 10, 2018)
>
>   Large file, listing communication frequencies for the airports in `airports.csv`.
>
> - [runways.csv](http://ourairports.com/data/runways.csv) (2,998,828 bytes, last modified Dec 10, 2018)
>
>   Large file, listing runways for the airports in `airports.csv`.
>
> - [navaids.csv](http://ourairports.com/data/navaids.csv) (1,539,725 bytes, last modified Dec 10, 2018)
>
>   Large file, listing worldwide radio navigation aids.
>
> - [countries.csv](http://ourairports.com/data/countries.csv) (20,386 bytes, last modified Dec 10, 2018)
>
>   A list of the world's countries. You need this spreadsheet to interpret the country codes in the airports and navaids files.
>
> - [regions.csv](http://ourairports.com/data/regions.csv) (365,815 bytes, last modified Dec 10, 2018)
>
>   A list of all countries' regions (provinces, states, etc.). You need this spreadsheet to interpret the region codes in the airport file.



根据csv的第一行为字段名建表

id设为int主键

其他全部设置为默认的varchar(255) 

airports的keywords有几条记录超过255了，设置为512（导入后select max(length(keywords) from airports 验证发现最长的记录是260+）

分表整理成mysql语句

[airport.sql.zip](airport.sql.zip)



## 字段含义

### airports.csv

#### id 

#### ident

对应机场四字码 icao_code

http://airport.anseo.cn/

> ### 机场四字代码简介
>
> 机场四字代码亦称ICAO机场代码、国际民航组织机场代码，其全称为国际民间航空组织机场代码（International Civil Aviation Organization Airport Code，缩写 ICAO code），是国际民航组织为世界上所有机场所订定的识别代码，由四个英文字母组成。ICAO 机场代码较少在公众使用，主要用于空中交通管理部门之间传输航班动态，通常用於空中交通管理及飞行策划等。
>
> 国际民间航空组织机场代码与一般公众及旅行社所使用的IATA机场代码并不相同。
>
> 机场四字代码（国际民间航空组织机场代码）有区域性的结构，不会重复使用。通常首字母代表所属大洲，第二个字母则代表国家，剩余的两个字母则用于分辨城市。部分幅员广大的国家，则以首字母代表国家，其余三个字母用于分辨城市。

#### type 

机场类型

small_airport 小型机场

medium_airport  中型机场

large_airport 大型机场

closed 已关闭

heliport  直升飞机场

seaplane_base

balloonport



#### continent

七大洲

https://www.whatarethe7continents.com/

> **7 Continents:** The most commonly accepted number of continents is 7. North America, South America, Africa, Antarctica, Australia (Oceania), Europe, and Asia.

https://baike.baidu.com/item/%E4%B8%83%E5%A4%A7%E6%B4%B2/2565080?fr=aladdin

> **七大洲**指地球[陆地](https://baike.baidu.com/item/%E9%99%86%E5%9C%B0/1697358)分成的七大陆地板块，包括[亚洲](https://baike.baidu.com/item/%E4%BA%9A%E6%B4%B2/133681)（全称亚细亚洲）（Asia）、[欧洲](https://baike.baidu.com/item/%E6%AC%A7%E6%B4%B2/145550)（全称欧罗巴洲 ）（Europe）、[北美洲](https://baike.baidu.com/item/%E5%8C%97%E7%BE%8E%E6%B4%B2/135465)（全称北亚美利加洲）（North America）、[南美洲](https://baike.baidu.com/item/%E5%8D%97%E7%BE%8E%E6%B4%B2/138913)（全称南亚美利加洲） （South America）[非洲](https://baike.baidu.com/item/%E9%9D%9E%E6%B4%B2/81619)（全称阿非利加洲）（Africa）、[大洋洲](https://baike.baidu.com/item/%E5%A4%A7%E6%B4%8B%E6%B4%B2/195695)（Oceania）、[南极洲](https://baike.baidu.com/item/%E5%8D%97%E6%9E%81%E6%B4%B2/361230)（Antarctica）

North America (NA)  北美洲（全称北亚美利加洲）

South America (SA)  南美洲（全称南亚美利加洲）

Antarctica(AN)  南极洲

Europe(EU)  欧洲（全称欧罗巴洲 ）

Asia(AS)  亚洲  ( 全称亚细亚洲)

Africa(AF)  非洲（全称阿非利加洲）

Australia(OC)  大洋洲

NA-北美洲 SA-南美洲 AN-南极洲 EU-欧洲 AS-亚洲 AF-非洲 OC-大洋洲

#### iata_code

国际航空运输协会机场代码（International Air Transport Association airport code，缩写 IATA code）

http://airport.anseo.cn/

> ### 机场三字代码简介
>
> 我们俗称的机场三字代码、IATA 机场代码，其全称为国际航空运输协会机场代码（International Air Transport Association airport code，缩写 IATA code），是一个由国际航空运输协会规定、用于代表全世界大多数机场的代码。它的编号规则由三位英文字母组成，不允许有数字。多用于对公众的场合，最常见在登机证及行李牌上。
>
> 这些代码的分配由国际航空运输协会第763号决议决定，并且由在蒙特利尔的国际航空运输协会总部管理。这些代码每半年一次出版在IATA的航空公司编码目录里。但在大多数国家的正式航空刊物里，她们都使用国际民航组织机场代码而非国际航空运输协会机场代码。



## 整合需要的信息到一张表

```sql

CREATE TABLE `airport_info` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `icao_code` varchar(255) DEFAULT NULL COMMENT '四字码 国际民间航空组织机场代码 International Civil Aviation Organization Airport Code',
  `iata_code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL COMMENT '机场名称',
  `type` varchar(255) DEFAULT NULL COMMENT '机场类型',
  `latitude_deg` varchar(255) DEFAULT NULL COMMENT '纬度',
  `longitude_deg` varchar(255) DEFAULT NULL COMMENT '经度',
  `elevation_ft` varchar(255) DEFAULT NULL COMMENT '海拔 英尺',
  `continent` varchar(255) DEFAULT NULL COMMENT 'NA-北美洲 SA-南美洲 AN-南极洲 EU-欧洲 AS-亚洲 AF-非洲 OC-大洋洲',
  `country_code` varchar(255) DEFAULT '' COMMENT '国家代码',
  `country_name` varchar(255) DEFAULT NULL COMMENT '国家名称',
  `region_code` varchar(255) DEFAULT NULL COMMENT '州/省 代码',
  `region_name` varchar(255) DEFAULT NULL COMMENT '州/省 名称',
  `municipality` varchar(255) DEFAULT NULL COMMENT '市 名称',
  `scheduled_service` varchar(255) DEFAULT NULL,
  `gps_code` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```




```sql
insert into airport_info(icao_code,iata_code,type,name,latitude_deg,longitude_deg,
elevation_ft,continent,country_code,country_name,
region_code,region_name,municipality,scheduled_service,gps_code)
(
SELECT
	a.ident AS icao_code,
	a.iata_code,
	a.type,
	a. NAME,
	a.latitude_deg,
	a.longitude_deg,
	a.elevation_ft,
	a.continent,
	a.iso_country as country_code,
	c.name as country_name,
	a.iso_region as region_code,
	r.`name` as region_name,
	a.municipality,
	a.scheduled_service,
	a.gps_code
FROM
	airports a
	LEFT JOIN countries c ON a.iso_country=c.code
	LEFT JOIN regions r on a.iso_region=r.code
)
```

受影响的行: 54822
时间: 85.897s



再把整合的记过到处文件

[airport_info.sql.zip](airport_info.sql.zip)



