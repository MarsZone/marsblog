---
title: Spring-Security6.0
date: 2024-03-21 09:05:28
tags:
---

Spring Security 6引入了很多破坏性的更新，包括废弃代码的删除，方法重命名，全新的配置DSL等，但是架构和基本原理还是保持不变的。

本质上，Spring Security的实现原理很简单，就是提供了一个用于安全验证的Filter。

```
public class SimpleSecurityFilter extends HttpFilter {
    @Override
    protected void doFilter(HttpServletRequest request, HttpServletResponse response, FilterChain chain) throws IOException, ServletException {
        UsernamePasswordToken token = extractUsernameAndPasswordFrom(request);  // (1)
        if (notAuthenticated(token)) {  // (2)
            // 用户名密码错误
            response.setStatus(HttpServletResponse.SC_UNAUTHORIZED); // HTTP 401.
            return;
        }
        if (notAuthorized(token, request)) { // (3)
            // 当前登录用户的权限不足
            response.setStatus(HttpServletResponse.SC_FORBIDDEN); // HTTP 403
            return;
        }
        // 通过了身份验证和权限校验，继续执行其它Filter，最终到达Servlet
        chain.doFilter(request, response); // (4)
    }
}
```

在安全领域，由于攻防手段的多样性和认证鉴权方式的复杂性，将所有功能都放在一个Filter中会导致该Filter迅速演变为一个庞大而复杂的类。
因此，在实际应用场景中，我们常常将这个庞大的Filter拆分成多个小Filter，并将它们链接在一起。每个Filter都只负责特定领域的功能，比如CsrfFilter，AuthenticationFilter，AuthorizationFilter等
这种概念被称为FilterChain，实际上JarkataEE规范也有相识的概念。通过使用FilterChain，你就可以以插拔的方式添加或移除特定功能的Filter，而无需改动现有的代码。


[一文带你读懂Spring Security 6.0的实现原理](https://spring4all.com/forum-post/4256.html)