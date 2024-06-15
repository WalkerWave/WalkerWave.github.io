---
layout: post
title: kubernetes informer 机制详解
excerpt_image: https://github.com/huziuncle/huziuncle.github.io/blob/master/assets/images/k8s/k8s.png?raw=true
categories: Kubernetes
tags: [Kubernetes]
---

![banner](https://github.com/huziuncle/huziuncle.github.io/blob/master/assets/images/k8s/k8s.png?raw=true)

## 简介
Kubernetes Informer 机制是 Kubernetes 客户端库（Client-Go）中的一个重要组件，用于监控和缓存 Kubernetes API 对象的变化。

Informer 提供了一种高效、可靠的方式来跟踪 Kubernetes 集群中的资源状态，并在资源发生变化时触发相应的处理逻辑。

## 实现机制
![informer](https://github.com/huziuncle/huziuncle.github.io/blob/master/assets/images/k8s/informer.png?raw=true)

## 工作流程
![informer-seq](https://github.com/huziuncle/huziuncle.github.io/blob/master/assets/images/k8s/informer-seq.png?raw=true)

## 作用
+ 减少 API Server 压力：通过本地缓存避免频繁访问 API Server，从而减少 API Server 的压力。
+ 实时性：通过 Watch 机制，Informer 可以及时获取资源对象的变化，确保数据的实时性。
+ 简化开发：Informer 提供了便捷的接口，开发者可以方便地监听资源对象的变化并进行处理，简化了 Kubernetes 应用的开发。
