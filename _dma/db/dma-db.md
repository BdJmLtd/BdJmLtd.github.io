---
title:  "数据库表"
sequence: 102
---

- 供水量：

4203

## 数据库和用户

创建数据库（`jm_dma_db`）：

```text
CREATE DATABASE `jm_dma_db`;
```

创建用户（`jinma`）并授权：

```text
CREATE USER 'jinma'@'%' IDENTIFIED BY '123456';
GRANT ALL PRIVILEGES ON jm_dma_db.* TO 'jinma'@'%';
FLUSH PRIVILEGES;
```

## 数据表

```text
USE `jm_dma_db`;

SHOW FULL TABLES;
```

### DMA分区表

```text
DROP TABLE IF EXISTS `biz_district`;

CREATE TABLE `biz_district` (
  `id` BIGINT NOT NULL COMMENT '区域ID',
  `district_name` VARCHAR (255) NOT NULL COMMENT '区域名称',
  `parent_id` BIGINT DEFAULT 0 COMMENT '父级区域（一级区域，值为0）',
  `address` VARCHAR (200) COMMENT '地址',
  `shape` VARCHAR (900) COMMENT '多边形坐标',
  `memo` VARCHAR (2000) COMMENT '备注',
  `order_number` INT DEFAULT 0 COMMENT '排序',
  `version` INT DEFAULT 0 COMMENT '乐观锁',
  `del_flag` INT DEFAULT 0 COMMENT '删除标记;0 未删除 1 已删除',
  `created_by` VARCHAR (32) COMMENT '创建人',
  `created_time` DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_by` VARCHAR (32) COMMENT '更新人',
  `updated_time` DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (id)
) COMMENT = 'DMA分区';
```

- DMA分区ID
- DMA分区编号：001
- DMA分区名称：绵阳分区
- 人
  - 服务区人口（单位：人）
  - 用户数量（单位：户）
- 区域
  - 服务面积（单位：平方米）
- 高程
  - 区域最高高程（单位：米）
  - 区域最低高程（单位：米）
- 管线
  - 材质
    - 管材分类（不明确）
  - 数量
    - 进入区域的管线数量（单位：条）
    - 管道连接总数（单位：个）
  - 时间：
    - 管道最长服务年限（单位：年）
  - 长度
    - 管道总长度（单位：米）
    - 私人拥有水管长度（单位：米）
  - 事故
    - 区域每年爆管数量（单位：次）
- 用水量
  - 日售水量（单位：立方米）
  - 无计量用水（单位：立方米）
  - 正常夜间用水量（单位：立方米）
  - 夜间允许最小流量（单位：立方米/小时）
  - 预期供水量
- 管理目标
  - 目标比例（范围0~100%，例如15%，这里计算的是“漏失率”，就是物理漏水量占总供水量的比例 ）
- 操作人
  - 修改者（用户姓名）
  - 修改时间（YYYY-MM-dd HH:mm）

> 参考自《分区定量管理理论与实践》（第二版） P126

