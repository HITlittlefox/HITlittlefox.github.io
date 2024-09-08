---
title: JWT And Authentication
category: Backend
date: 2024-08-31 11:25:08
tags: JWT
---

# Authentication

1. JWT Authentication
2. [Token based Authentication](https://roadmap.sh/guides/token-authentication)
3. Session based Authentication
4. Basic Authentication
5. [OAuth - Open Authorization](https://developer.okta.com/blog/2017/06/21/what-the-heck-is-oauth)
    1. OAuth 是：
        1. 应用程序请求用户授权
        2. 用户授权 App 并交付证明
        3. 应用程序向服务器提供授权证明以获取令牌
        4. Token 仅限于访问用户为特定 App 授权的内容
    2. OAuth 2.0 摘要
        1. OAuth 2.0 是一个授权框架，用于委派对 API
           的访问。它涉及请求资源所有者授权/同意的范围的客户端。授权授权将交换访问令牌和刷新令牌（取决于流程）。有多个流程可以处理不同的客户端和授权场景。JWT
           可用于 Authorization Server 和 Resource Server 之间的结构化令牌。
        2. OAuth 具有非常大的安全外围应用。确保使用安全的工具包并验证所有输入！
        3. OAuth 不是身份验证协议。OpenID Connect 扩展了 OAuth 2.0 以用于身份验证方案，通常称为“带大括号的 SAML”。
6. SSO - Single Sign On

# JWT

1. authorization AND authenticate

# 