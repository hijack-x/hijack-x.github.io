---
layout: post
title: 使用autoconf和automake生成Makefile
date: 2014-06-04 22:30:00
categories: article
---

1、创建hello.c文件，内容如下：
```#include <stdio.h>

int main(int argc, char **argv)
{
    printf("Hello!\n");
    return 0;
}
```

2、创建Makefile.am文件，内容如下：
```
AUTOMAKE_OPTIONS=foreign 
bin_PROGRAMS=hello 
hello_SOURCES=hello.c
```

3、执行autoscan，生成configure.scan，重命名为configure.in并修改：
```
#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.63])
#AC_INIT([FULL-PACKAGE-NAME], [VERSION], [BUG-REPORT-ADDRESS])
AC_INIT([hello], [1.0], [bug@example.com])
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([hello.c])
#AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CC

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
```

4、执行aclocal，生成aclocal.m4文件

5、aotoconf，生成configure文件

6、执行automake --add-missing，生成Makefile.in文件
