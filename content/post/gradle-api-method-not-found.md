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
使用Gradle构建多模块项目，子模块A依赖于子模块B，并且A、B都需要用同一jar包。替换`implementation`为`api`时报错：

> Could not find method api() for arguments [org.springframework.boot:spring-boot-starter-data-jpa] on object of type org.gradle.api.internal.artifacts.dsl.dependencies.DefaultDependencyHandler.

【[使用的正确姿势](https://stackoverflow.com/questions/49543618/why-isnt-api-method-available-in-gradle-4-4-java-plugin-when-implementation) 】，改为应用` java-library`插件即可。

{{< codeblock "build.gradle" "diff" "" "" >}}
- apply plugin: 'java'
+ apply plugin: 'java-library'
{{< /codeblock >}}
