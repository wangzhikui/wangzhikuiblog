---
title: sql语句：将结果中的数字转为汉字使用case语句
categories: 笔记
tags: [笔记,sql]
date: 2019-01-16
---

# <font color="green" >case语句</font>
```sql
SELECT
	st.`name` AS 名称 ,
	st.email AS 申请人邮箱 ,
	st.phone AS 申请人电话 ,
	(
		CASE st.`status`
		WHEN 0 THEN
			'未审核'
		WHEN 1 THEN
			'试用'
		WHEN 2 THEN
			'开通'
		WHEN 8 THEN
			'驳回'
		WHEN 9 THEN
			'停用'
		ELSE
			'null'
		END
	) 状态
FROM
	s_table st
WHERE
	dr = 0

```