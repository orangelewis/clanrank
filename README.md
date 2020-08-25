# clanrank
 适用于HoshinoBot v2的插件, 可以在群聊中查询公会战排名（仅B服）. 

数据均来自Github@Kengxxiao

项目地址 https://github.com/Kengxxiao/Kyouka

网页在线查询 https://kengxxiao.github.io/Kyouka/

本项目地址 https://github.com/pcrbot/clanrank

本插件以HoshinoBot v2为基础编写, 使用HoshinoBot v1请切换至v1分支. 注意, v1版本可能无法得到及时更新和测试, 如果您正在使用HoshinoBot的v1版本, 并修改本插件使其适配v1, 希望您能向本项目的v1分支提交Pull request

如果发生400/441错误, 可能是更新了POST请求头, 请更新或等待更新. 出现404错误则是公会不在列表中, 可能的原因:
1. 会长在农场, 或会长已换人
2. 公会已解散
3. 公会排名不在前2W名
4. 不是B服公会

现已更新缓存机制, ~~v0.1.5版本由于源站时间戳变更暂时失效, 请适度查询~~ 已修复

假定网站更新比游戏内延迟12分钟, 则每次查询的时间戳生命周期为42分钟, 如果没有过期则只需要发送本机缓存的数据. 请限制使用频率, 为了不给原作者服务器增加太大负担 

例如, 缓存的上次查询的时间戳为下午3点, 则下午3:42之前查询会发送本地数据, 3:42之后查询会自动在线更新.


## 指令示例
### 查询所有公会（需开启服务:clanrank-query）
* 查询会长卢本伟, 查询会长名字包含卢本伟的公会的排名
* 查询公会卢本伟, 查询公会名字包含卢本伟的公会的排名
* 查询排名5000, 查看5000名的公会分数信息
* 分数线, 查询分数线
### 查询自己公会（需开启服务:clanrank-push）
* 绑定公会12345567889, 后加的是公会会长的ID
* 公会排名, 查询本公会排名
## 使用方法
1. ~~加入其他模块中~~
    
    不再支持此方法, 因为配置文件使用了以下路径来读写:
    ```
    ./hoshino/modules/clanrank/clanrank.json
    ```
2. 创建新目录, 作为一个单独的模块来控制. 切换到Hoshino的模组目录, 然后clone本项目:
    ```
    git clone https://github.com/pcrbot/clanrank.git
    ```
    修改配置文件:在config中启用该模块. 操作方法为编辑Hoshino下的`__bot__.py`文件:
    ```
    nano ~/Hoshino/hoshino/config/__bot__.py
    ```
    在`MODULES_ON`中仿照格式添加项`'clanrank'`. 
3. HoshinoBot v1版本请直接克隆`v1`分支:
   ```
   git clone -b v1 https://github.com/pcrbot/clanrank.git
   ```
4. 更新请切换到对应目录后, 使用git更新:
   ```
   git pull
   ```
   如果要更换分支:
   ```
   git checkout -b 本地分支名 origin/v1
   ```
## TODO
 - [x] 增加缓存机制, 减少调用次数
 - [x] 加入line接口
 - [x] 加入fav接口
 - [x] 加入时间查询参数来查询历史分数
 - [ ] 分数线预测/拟合/数据分析
 - [ ] 分数线制图
## 更新日志:

### v0.1.5
更新时间: 2020/8/24 8:52
* 移除消息模板中的人数, 因源站已不再返回
* 修改了指令帮助【绑定公会】
* ~~已知问题:查询缓存机制不启用, 且每次显示的更新时间为1970年, 原因是源站返回的ts值为0, 等待进一步适配~~ 已修复
* 适配v1, 来自群友Stranger, 在此感谢

### v0.1.4
更新时间: 2020/8/01 20:45
* 新增line接口, 查询分数线（共14条信息）
* 信息播报模板化, 可在`msg_temp.py`中自由配置
* POST请求增加最大超时, 提高稳定性

### v0.1.2
更新时间: 2020/8/01 13:30
* 非公会战期间不会自动每日推送排名
  
### v0.1.1
更新时间: 2020/7/31 8:23
* 新增BOSS进度条, 来自群艾琳佬
* 修正v1版本导入了不存在的`hoshino.typing`的问题, 同时删除了v2版多余的导入
* 更换示例的地址为pcrbot组织下的永久地址

### v0.1.0
更新时间: 2020/7/30 16:00
* 新增fav接口, 以会长ID查询
* 新增绑定公会信息, 以及每日推送公会排名
* 新增缓存机制, 减少对源站的访问次数
* 更新指令说明

### v0.0.6
更新时间: 2020/7/30 9:08
* 修正header头
* 适配HoshinoV2
* 迁出v1分支, 适配Hoshinov1
* 修正`README.md`的问题
  
### v0.0.4
更新时间:2020/7/3 11:04
* 查询结果最后会显示数据更新时间

### v0.0.3
更新时间:2020/7/3 3:05
* 更新请求, 为所有查询时的POST请求添加"history"
* 添加了对BadRequest的处理, 可以半夜被叫起来修

### v0.0.2
更新时间:2020/7/1 12:22
* 更新请求, 为请求头添加"Referer"

### v0.0.1
更新时间:2020/6/30 2:19
* 初版发布, 支持四种查询模式

