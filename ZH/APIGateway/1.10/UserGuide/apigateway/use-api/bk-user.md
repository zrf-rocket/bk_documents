# 获取蓝鲸用户身份

访问云 API 时，若认证用户，校验用户身份，则需要提供代表用户身份的信息。

目前，网关支持的蓝鲸用户身份信息如下：
- 用户登录态：用户登录蓝鲸后，存储在浏览器 Cookies 中的用户登录凭证，一般有效期不超过 24 小时

## 用户登录态

用户登录蓝鲸后，在浏览器 Cookies 中会存储用户的登录凭证，此登录凭证，即可代表用户身份。

蓝鲸用户的登录态信息如下：

| 请求参数字段 | Cookies 字段 | 说明 |
|----------|--------------|------|
| bk_token | bk_token | 用户登录态 |
