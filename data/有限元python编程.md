@[TOC](<center>《有限元分析基础教程》（曾攀）二维杆单元有限元程序（MATLAB转Python）</center>)
<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# 前言

<font color=#999AAA >曾攀老师的《有限元分析基础教程》第三章有二维杆单元的推导，并结合一个例题进行了解析解和基于Matlab的程序求解。初学Python、MATLAB和有限元分析，于是我以自己的思路，基于Python翻译了这段程序，给也在学习有限元分析但电脑安装不上MATLAB的朋友提供一个思路。如有不足之处，敬请斧正。</font>

<font face = '宋体' color = black size = 5>**完成目标：**
&emsp;&emsp;在Pycharm上将MATLAB程序翻译为Python，执行代码，对比结果，最后总结。
		那么现在开始！！！

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# 一、
<font face = '宋体' color = black size = 5>

# 二、
- ## 代码如下，相关操作已说明

1. 先创建一个`Bar2D2Node.py`，再将下述代码输入。

```python
# !/usr/bin/env python 
# coding:utf-8
# 2D 杆单元的有限元分析程序
# Bar2D2Node # begin
import numpy as np


def Stiffness(el_mo, area, x1, y1, x2, y2, alpha):
    """
    该函数计算单元的刚度矩阵
    输入弹性模量(elastic_modulus)el_mo，横截面积area
    输入第一个节点坐标（x1,y1），第二个节点坐标（x2,y2），角度alpha（单位是度）
    输出单元刚度矩阵k(4X4)
    """
    length = np.sqrt((x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1))
    x_variable = alpha * np.pi / 180
    c = np.cos(x_variable)
    s = np.sin(x_variable)
    k = el_mo * area / length * np.array([[c * c, c * s, -c * c, -c * s],
                                          [c * s, s * s, -c * s, -s * s],
                                          [-c * c, -c * s, c * c, c * s],
                                          [-c * s, -s * s, c * s, s * s]])
    return k


def Assembly(kk, k, i, j):
    """
    该函数进行单元刚度矩阵的组装
    输入单元刚度矩阵k，单元的节点编号i、j
    输出整体刚度矩阵kk
    """
    dof = ([2 * i - 2, 2 * i - 1, 2 * j - 2, 2 * j - 1])
    for n1 in range(int(len(dof))):
        for n2 in range(int(len(dof))):
            kk[dof[n1], dof[n2]] += k[n1, n2]
    return kk


def Stress(el_mo, x1, y1, x2, y2, alpha, u):
    """
    该函数计算单元的应力
    输入弹性模量E，第一个节点坐标（x1,y1），第二个节点坐标（x2,y2）
    输入角度alpha（单位是度）和单位节点位移矢量u
    返回单元应力标量stress
    """
    length = np.sqrt((x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1))
    x_variable = alpha * np.pi / 180
    c = np.cos(x_variable)
    s = np.sin(x_variable)
    stress = el_mo / length * np.dot(np.array([-c, -s, c, s]), u)
    return stress


def Force(el_mo, area, x1, y1, x2, y2, alpha, u):
    """
    该函数计算单元的应力矩阵
    输入弹性模量E，横截面积A
    输入第一个节点坐标（x1,y1），第二个节点坐标（x2,y2），角度alpha（单位是度）
    输入单元节点位移矢量u
    返回单元节点力矩阵force
    """
    length = np.sqrt((x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1))
    x_variable = alpha * np.pi / 180
    c = np.cos(x_variable)
    s = np.sin(x_variable)
    force = el_mo * area / length * np.dot(np.array([-c, -s, c, s]), u)
    return force

# Bar1D2Node # end

```



## 2.

## 3.

## 4.

## 5.

## 6.

# 最后
><font face="宋体"  color = black size = 4>最后想和读者说的话