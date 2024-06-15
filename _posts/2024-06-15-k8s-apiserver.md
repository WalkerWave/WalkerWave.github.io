---
layout: post
title: kube-apiserver
categories: Kubernetes
tags: [k8s]
---

## kube-apiserver 初始化流程
@startmindmap
!theme toy

* api-server

** API
*** Aggregator
**** APIServer的Discovery功能

*** KubeAPIServer
**** 内建资源的REST服务

*** APIExtensionServer
**** CRD资源服务器

** 流程

*** CreateServerChain
**** apiExtensionsServer
***** genericServer
****** apiextensions.k8s.io
****** customresourcedefinition.NewREST
****** customresourcedefinition.NewStatusREST
****** InstallAPIGroup
******* installAPIResources
******** getAPIGroupVersion

********* InstallREST
********** APIInstaller
*********** Install
************ newWebService
************ registerResourceHandlers
************* route: path <-> handler: storage.(rest.Creater|Lister|Getter|Updater|Patcher|Watcher|...)
************* WebService.Route

********* container.Add(ws)

***** NewCustomResourceDefinitionHandler
****** 注册crd处理请求到api路由

***** 启动informer
***** 启动控制器
****** namingController
****** establishingController
****** nonStructuralSchemaController
****** apiApprovalController
****** finalizingController
****** discoveryController


**** kubeAPIServer
***** ControlPlane
****** genericServer
******* SharedInformerFactory.Start
******* FlowControl
******* StorageObjectCountTracker

****** namespacesController
****** peerEndpointController
****** clusterAuthenticationTrustController
****** legacytokentrackingController

***** InstallAPIs -> restStorageProviders
****** InstallLegacyAPIGroup
******* installAPIResources
****** InstallAPIGroups
******* installAPIResources

***** bootstrapController
***** cidrController



**** aggregatorServer


*** filter chain
**** 认证、鉴权

*** handler
**** Decode
***** 将用户资源版本转换为内部资源版本

**** Admission
***** 全局约束插件
****** ValidatingAdmissionWebhook
****** MutatingAdmissionWebhook

**** Validation
***** 检查object的合法性


@endmindmap
