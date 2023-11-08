# appstore

适配[1Panel](https://github.com/1Panel-dev/1Panel) 应用商店

- 悟空 IM
- 唐僧叨叨

# local-appstore-for-1Panel

## 使用教程

### 1. 使用 1Panel 创建计划任务

![new_cron_task](https://raw.githubusercontent.com/xxxily/local-appstore-for-1Panel/main/docs/img/new_cron_task.png)

按上图方式创建计划任务。

然后将 [local_appstore_sync_helper.sh](https://github.com/xxxily/local-appstore-for-1Panel/blob/main/local_appstore_sync_helper.sh) 内容复制到脚本内容框中。

按需修改脚本中的配置项，具体的配置项说明见下文。

### 2. 执行同步脚本

点击执行按钮，可即可开始同步。

![run_cron_task](https://raw.githubusercontent.com/xxxily/local-appstore-for-1Panel/main/docs/img/run_cron_task.png)

### 3. 查看同步脚本的执行情况

点击任务名称或【报告】按钮即可查看同步脚本的执行日志。

![run_cron_task_result](https://raw.githubusercontent.com/xxxily/local-appstore-for-1Panel/main/docs/img/run_cron_task_result.png)

注意：目前 1Panel 的计划任务执行失败的话查看不了任何日志，这个时候去【主机】>【文件】然后进入：

`/opt/1panel_hepler/logs`

目录下查看同步脚本的执行日志即可。

## 配置项详解

[local_appstore_sync_helper.sh](https://github.com/TangSengDaoDao/appstore/master/local_appstore_sync_helper.sh) 里包含了一些配置项，可以根据自己的需求进行修改。

```bash
# 1panel本地app的目录（如果不是默认安装，需修改该目录）
app_local_dir="/opt/1panel/resource/apps/local"

# AppStore的git仓库地址（必选）
git_repo_url="https://github.com/TangSengDaoDao/appstore"

# 访问git仓库的access token，访问私有仓库时用，优先级高于账密（可选）
# 建议使用access token，降低账密泄露的风险
git_access_token=""

# 访问git仓库的用户名，访问私有仓库时用（可选）
git_username=""
# 访问git仓库的密码，访问私有仓库时用（可选）
git_password=""

# 指定克隆的分支（可选）
git_branch=""
# 指定克隆的深度（可选）
git_depth=1

# 拉取远程仓库前是否清空本地app目录（可选）
clean_local_app=false
# 拉取远程仓库前是否清空远程app缓存（可选）
clean_remote_app_cache=false

# 设置克隆或拉取远程仓库时使用的代理（可选）
proxyUrl=""
# 设置示例：
# proxyUrl="http://127.0.0.1:7890"
# proxyUrl="socks5://127.0.0.1:7890"
# proxyUrl="socks5://user:password@host:port"

# 将远程app store工程克隆到本地的工作目录
work_dir="/opt/1panel_hepler"
```

各个配置项的具体说明如下：

| 配置项 | 必选 | 使用说明 |
| ---: | :---: | :--- |
| app_local_dir | 是 | 1Panel本地app的目录（如果不是默认安装，需修改该目录） |
| git_repo_url | 是 | AppStore的git仓库地址，直接复制链接地址即可，脚本会自动补充链接需要的字段 |
| git_access_token | 否 | 访问git仓库的access token，访问私有仓库时用，优先级高于账密 |
| git_username | 否 | 访问git仓库的用户名，访问私有仓库时用 |
| git_password | 否 | 访问git仓库的密码，访问私有仓库时用；脚本已增加了对特殊字符的支持 |
| git_branch | 否 | 指定克隆的分支，不指定则使用仓库的默认分支 |
| git_depth | 否 | 指定克隆的深度，层级越多克隆越慢，建议默认即可 |
| clean_local_app | 否 | 拉取远程仓库前是否清空本地app目录，可以把不需要旧应用清除掉，保持跟线上的一致<br />如果要同步多个仓库的应用，则必须设定为`flase`，否则只会看到最后一个的同步结果 |
| clean_remote_app_cache | 否 | 拉取远程仓库前是否清空远程app缓存，相当于重新clone远程app仓库 |
| proxyUrl | 否 | 设置克隆或拉取远程仓库时使用的代理，一般来说国内克隆GitHub仓的时候用得到 |
| work_dir | 是 | 将远程app store工程克隆到本地的工作目录，用于临时存放克隆下来的文件和脚本工作日志 |