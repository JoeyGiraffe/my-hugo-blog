---
title: "Could not find method api() for arguments"  
slug: gradle-api-method-not-found  
metaAlignment: center  
coverMeta: out  
date: 2019-03-06  
categories:
- tutorial
tags:
- gradle   
keywords:
- gradle
- api()
- java-library
---

注意：`Java Plugin`不包含 `api()`方法。
<!--more-->
使用`Gradle`构建多模块项目，子模块`repository`依赖于`entity`，并且两者都需要用到`spring-boot-starter-data-jpa`。替换 `implementation` 为 `api` 时报错：

> Could not find method api() for arguments [org.springframework.boot:spring-boot-starter-data-jpa] on object of type org.gradle.api.internal.artifacts.dsl.dependencies.DefaultDependencyHandler.

查了个把小时才找到【[使用的正确姿势](https://stackoverflow.com/questions/49543618/why-isnt-api-method-available-in-gradle-4-4-java-plugin-when-implementation) 】，改为应用` java-library`插件即可。










