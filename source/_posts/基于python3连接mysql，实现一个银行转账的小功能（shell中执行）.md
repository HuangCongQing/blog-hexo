---
title: 基于python3连接mysql，实现一个银行转账的小功能（shell中执行）
date: 2017-07-31 17:50:33
tags: [python, MySQL]
---

基于python3连接mysql，实现一个银行转账的小功能（shell中执行）

准备工作：首先我创建了
* imooc的数据库
* 名字为account的表
* 表里面键值（acctid,money）
<!-- more -->
* 下面是代码：
```
# -*- coding: utf-8 -*-
# @Author: hasee
# @Date:   2017-11-02 21:30:11
# @Last Modified by:   重庆
# @Last Modified time: 2017-11-02 21:30:43
#coding=utf-8
import pymysql 
import sys 
class TransferMoney: 
    def __init__(self,conn): 
        self.conn = conn 
    def check_acct_available(self, acctid): 
        try: 
            cursor = self.conn.cursor() 
            sql = "select * from account where acctid= %s " % acctid 
            cursor.execute(sql) 
            print ("check_acct_available:" + sql) 
            rs = cursor.fetchall() 
            if len(rs) != 1: 
                raise Exception("账号%s 不存在" % acctid) 
        finally:
            cursor.close() 
                
    def has_enough_money(self, acctid, money): 
        try: 
            cursor = self.conn.cursor() 
            sql = "select * from account where acctid=%s and money>=%s" % (acctid,money) 
            cursor.execute(sql) 
            print ("has_enough_money:" + sql) 
            rs = cursor.fetchall() 
            if len(rs) != 1: 
                raise Exception("账号%s余额不足 is not enough" % acctid) 
        finally: 
            cursor.close() 
    def reduce_money(self, acctid, money): 
        try: 
            cursor = self.conn.cursor() 
            sql = "update account set money= money-%s WHERE acctid=%s " % (money,acctid) 
            cursor.execute(sql) 
            print ("reduce_money:" + sql) 
            rs = cursor.rowcount 
            if rs != 1: 
                raise Exception("账号%s付款失败Eend is not enough" % acctid) 
        finally: 
            cursor.close() 
    def add_money(self, acctid, money): 
        try: 
            cursor = self.conn.cursor() 
            sql = "update account set money= money+%s WHERE acctid=%s " % (money,acctid) 
            cursor.execute(sql) 
            print("add_money:" + sql) 
            rs = cursor.rowcount 
            if rs != 1: 
                raise Exception("账号%s收款失败(Payment failure)get is not enough" % acctid) 
        finally: 
            cursor.close() 
    def transfer(self, source_acctid, target_acctid, money): 
        try: 
            self.check_acct_available(source_acctid) 
            self.check_acct_available(target_acctid) 
            self.has_enough_money(source_acctid,money) 
            self.reduce_money(source_acctid,money) 
            self.add_money(target_acctid,money) 
            self.conn.commit() 
        except Exception as e: 
            self.conn.rollback() 
            raise e 
if __name__=="__main__": 
    ## print("sys.argv[1:]:",sys.argv[1:])
    source_acctid = sys.argv[1] # 汇款发送账户
    target_acctid = sys.argv[2] # 收款账户
    money = sys.argv[3] 
    conn = pymysql.connect( 
        host = '127.0.0.1', 
        port = 3306, 
        user = 'root', 
        passwd = '123456', 
        db = 'imooc', 
        charset = 'utf8' ) 
    tr_money = TransferMoney(conn) 
    try: 
        tr_money.transfer(source_acctid,target_acctid,money) 
    except Exception as e: 
        print("出现问题(There is a problem)：" + str(e)) 
    finally: 
        conn.close()


```
注意此代码只能在shell命令行中运行，否则会报类似如下错误：
`sys.argv[3] IndexError: list index out of range`

![IndexError](http://upload-images.jianshu.io/upload_images/4340772-bca9a728af8d951a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

原因是：需要在命令行输入参数，否则，就会报错

### 下面是运行结果（账户1转给账户2一共3元钱）
在XXX.py(mysqlAccount.py)文件目录下运行

`python mysqlAccount.py 1 2 3`

![转账前](http://upload-images.jianshu.io/upload_images/4340772-70e28e22d882dde6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/4340772-11280a0ef7fadd9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![转账后](http://upload-images.jianshu.io/upload_images/4340772-b1230c98772886f6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
好看的人儿，点个喜欢❤ 你会更好看哦~~
