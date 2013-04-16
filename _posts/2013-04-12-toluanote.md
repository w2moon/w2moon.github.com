---
layout: post
title: "new day"
description: ""
category: 
tags: []
---
{% include JB/setup %}


问题
lua_pushliteral什么用
lua_pushcclosure，最后一个参数n什么用
lua_pushvalue的用途,把指定索引值放到栈顶

tolua绑定方式
1、tolua系统LUA_REGISTRYINDEX里放一个值表示是否初始化过
2、没初始化过则执行初始后逻辑，并设置LUA_REGISTRYINDEX里的值
3、创建基本的tolua_ubox table
4、新建table，设置为weaktable(__mode设为v)，以便userdata的垃圾收集
5、把新建的表设为基本table的元表
6、设置tollua_ubox到LUA_REGISTRYINDEX中
7、再在LUA_REGISTRYINDEX里建两个新表tolua_super，tolua_gc
8、设tolua_super的closure为class_gc_event
9、建立新的tolua_commonclass为metatable，设到LUA_REGISTRYINDEX里，注册__index，__call等参数
10、给tolua_gc_event注册__gc

第一：编写 C 库的时候，完全针对 lua 设计，所有对象都有 lua_newuserdata 分配内存。对象和对象之间的联系可以使用 userdata 的 环境表，把对象间的引用放在里面，使得 lua 的 gc 过程可以正常进行。

第二：给 C 对象简单加一个壳。lua 的 userdata 中仅仅保存 C 对象指针。然后给 userdata 设置 gc 元方法，在被回收时，正确调用 C 对象的销毁函数。

有我们在使用之前包括下面的定义：

typedef double real;

否则，real将会被解释为用户定义类型而不会映射到Lua的number类型。

tolua++ fix
luabind的绑定方式
tolua++package自动生成