# 安全世界观

#### 安全的本质

——信任问题

* 信任域
* 信任边界
* 安全检查

#### 安全三要素

* 机密性
* 完整性
* 可用性

#### 安全评估

1. ##### 资产等级划分

2. ##### 威胁分析

   * ###### 威胁建模

     * STRIDE
       * Spoofing伪装
       * Tampering篡改
       * Repudiation抵赖
       * InformationDisclosure信息泄露
       * Denial of Service拒绝服务
       * Elevation of Privilege提升权限

3. ##### 风险分析

   * DREAD
     * Damage Potential（潜在危害）
     * Reproducibility（再现性）
     * Exploitability（可利用性）
     * Affected users（受影响的用户）
     * Discoverability（可发现性）

4. ##### 确认解决方案

### 白帽子兵法

##### Secure By Default原则

* 白名单
* 最小权限原则

##### 纵深防御原则

##### 数据与代码分离原则

##### 不可预测性原则

* 克服攻击方法

***

# 客户端脚本安全

## 浏览器安全

#### 同源策略

###### 影响源的因素

* host
* 子域名
* 端口
* 协议

> 页面内存放js文件的域不重要，重要的是加载 js页面所在的域
>
> ```html
> <!--a.com通过以下代码加载b.js-->
> <script src=http://b.com/b.js></script>
> <!--b.js的源是a.com而非b.com-->
> ```

> 浏览器中`<script><img><iframe><link>`等标签都可以跨域加载资源，不受同源策略的限制。这些带“src”属性的标签每次加载时，浏览器发起了一次GET请求。
>
> 通过src属性加载的资源，浏览器限制了JavaScript的权限，使其__不能读、写返回的内容__。

Q： p 30

#### 浏览器沙箱