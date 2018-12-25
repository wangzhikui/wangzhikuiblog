---
title: SQLServer 导出数据的存储过程
categories: 数据库
tags: [SQLServer,数据库]
date: 2012-01-18
---
``` sql
declare @objectId int 
set @objectId=object_id('proc_insert') 
if @objectId is not null 
begin 
    drop proc proc_insert 
end 
go 

create proc proc_insert (@tablename varchar(256)) 
as 
begin 
    set nocount on 
    declare @sqlstr varchar(4000) 
    declare @sqlstr1 varchar(4000) 
    declare @sqlstr2 varchar(4000) 
    select @sqlstr='select ''insert '+@tablename 
    select @sqlstr1='' 
    select @sqlstr2='(' 
    select @sqlstr1='values (''+' 
    select @sqlstr1=@sqlstr1+col+'+'',''+' ,@sqlstr2=@sqlstr2+name +',' from (select case 
    when a.xtype =173 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar('+convert(varchar(4),a.length*2+2)+'),'+a.name +')'+' end' 
    when a.xtype =104 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(1),'+a.name +')'+' end' 
    when a.xtype =175 then 'case when '+a.name+' is null then ''NULL'' else '+'''''''''+'+'replace('+a.name+','''''''','''''''''''')' + '+'''''''''+' end' 
    when a.xtype =61 then 'case when '+a.name+' is null then ''NULL'' else '+'''''''''+'+'convert(varchar(23),'+a.name +',121)'+ '+'''''''''+' end' 
    when a.xtype =106 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar('+convert(varchar(4),a.xprec+2)+'),'+a.name +')'+' end' 
    when a.xtype =62 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(23),'+a.name +',2)'+' end' 
    when a.xtype =56 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(11),'+a.name +')'+' end' 
    when a.xtype =60 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(22),'+a.name +')'+' end' 
    when a.xtype =239 then 'case when '+a.name+' is null then ''NULL'' else '+'''''''''+'+'replace('+a.name+','''''''','''''''''''')' + '+'''''''''+' end' 
    when a.xtype =108 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar('+convert(varchar(4),a.xprec+2)+'),'+a.name +')'+' end' 
    when a.xtype =231 then 'case when '+a.name+' is null then ''NULL'' else '+'''''''''+'+'replace('+a.name+','''''''','''''''''''')' + '+'''''''''+' end' 
    when a.xtype =59 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(23),'+a.name +',2)'+' end' 
    when a.xtype =58 then 'case when '+a.name+' is null then ''NULL'' else '+'''''''''+'+'convert(varchar(23),'+a.name +',121)'+ '+'''''''''+' end' 
    when a.xtype =52 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(12),'+a.name +')'+' end' 
    when a.xtype =122 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(22),'+a.name +')'+' end' 
    when a.xtype =48 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar(6),'+a.name +')'+' end' 
    when a.xtype =165 then 'case when '+a.name+' is null then ''NULL'' else '+'convert(varchar('+convert(varchar(4),a.length*2+2)+'),'+a.name +')'+' end' 
    when a.xtype =167 then 'case when '+a.name+' is null then ''NULL'' else '+'''''''''+'+'replace('+a.name+','''''''','''''''''''')' + '+'''''''''+' end' 
    else '''NULL''' 
    end as col,a.colid,a.name 
    from syscolumns a where a.id = object_id(@tablename) and a.xtype <>189 and a.xtype <>34 and a.xtype <>35 and a.xtype <>36 
    )t order by colid 
    select @sqlstr=@sqlstr+left(@sqlstr2,len(@sqlstr2)-1)+') '+left(@sqlstr1,len(@sqlstr1)-3)+')'' from '+@tablename 
    print @sqlstr 
    exec( @sqlstr) 
    set nocount off 
end 
go 

exec proc_insert 'risk_item' 
```