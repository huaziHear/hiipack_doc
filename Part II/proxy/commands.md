# 指令 {#command}

`指令`（也称：`命令`）用于设置变量，或者对`request`\/`response`做一些操作。

## hiipack 支持的指令 {#supported-commands}

### 全局指令 {#global-commands}

> 全局指令，用来在全局作用域中做一些配置。

#### set {#set}

_作用_：定义变量

_参数_：

```bash
key：变量名称
value：值
```

_例子_：

```bash
set $server hiipack;
```

### 代理请求相关指令 {#res-scope}

> 代理请求相关的指令，用于操作代理服务向目标服务器发送请求的`Request`对象。

#### proxy\_pass {#proxy-pass}

_作用_：设置请求转发的目标地址

_参数_：

```bash
url：要转发的地址
```

_例子_：

```bash
proxy_pass http://some.example.com/some/path/;
```

#### proxy\_set\_header {#proxy-set-header}

_作用_：设置请求头部字段

_参数_：

```bash
key：字段名称
value：字段值
```

_例子_：

```bash
proxy_set_header Host some.example.com
```

#### proxy\_hide\_header {#proxy-hide-header}

_作用_：删除请求头部字段

_参数_：

```bash
key: 要删除的字段名称
```

_例子_：

```bash
proxy_set_header Host some.example.com
```

#### proxy\_set\_cookie {#proxy-set-cookie}

_作用_：设置请求Cookie

_参数_：

```bash
key：Cookie名称
value：Cookie值
```

_例子_：

```bash
proxy_set_cookie from hiipack;
```

#### proxy\_hide\_cookie {#proxy-hide-cookie}

_作用_：删除请求Cookie字段

_参数_：

```bash
key：Cookie名称
```

_例子_：

```bash
proxy_hide_cookie from;
```

### 代理响应相关指令 {#res-scope}

> 代理响应相关的指令用于配置代理服务器响应浏览器的`Response`对象。

#### set\_header {#set-header}

_作用_：添加Header字段

_参数_：

```bash
key：Header字段名称
value：Header字段的值
```

_例子_：

```bash
set_header SERVER HIIPACK;
```

#### hide\_header {#hide-header}

_作用_：删除Header字段

_参数_：

```bash
key：Header字段名称
```

_例子_：

```bash
hide_header Server;
```

#### set\_cookie {#set-cookie}

_作用_：设置Cookie字段

_参数_：

```bash
key：Cookie名称
value：Cookie值
```

_例子_：

```bash
set_cookie SESSION_ID 2BF36A09CB35FD71E;
```

#### hide\_cookie {#hide-cookie}

_作用_：删除Cookie字段

_参数_：

```bash
key：Cookie名称
```

_例子_：

```bash
hide_cookie SESSION_ID;
```

