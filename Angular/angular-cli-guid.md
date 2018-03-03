## Angular CLI 使用教程指南参考

Angular CLI 现在虽然可以正常使用但仍然处于测试阶段. Angular CLI 依赖 Node 4 和 NPM 3 或更高版本.

## 安装

要安装Angular CLI你需要先安装node和npm，然后运行以下命令来安装最新的Angular CLI：

注意：Angular CLI 需要Node 4.X 和 NPM 3.X 以上的版本支持。

```
npm install -g angular-cli
```

在 Mac 或 Linux 平台上，你可能需要添加  `sudo` 前缀提权进行全局安装： 

```
sudo npm install -g angular-cli
```

## 基本用法

你可以通过 Angular CLI 的  `help` 命令来获取相关的命令信息. 

```
ng help
```

Angular CLI的命令关键字为  `ng`

## ng new

| 命令                              | 描述                                           |
| --------------------------------- | ---------------------------------------------- |
| `ng new <project-name> [options]` | 创建一个新的 Angular 项目,默认在当前所在目录下 |

| 参数             | 描述                                                 |
| ---------------- | ---------------------------------------------------- |
| `--dry-run` `-d` | 只输出要创建的文件和执行的操作，实际上并没有创建项目 |
| `--verbose` `-v` | 输出详细信息                                         |
| `--skip-npm`     | 在项目第一次创建时不执行任何npm命令                  |
| `--name`         | 指定创建项目的名称                                   |

## ng serve

```
ng new PROJECT_NAME
cd PROJECT_NAME
ng serve
```

将会自动在浏览器中打开默认地址  `http://localhost:4200/` . 运行之后如果你修改了程序源代码.应用将会自动重载. 

你也可以自定义配置 IP, 端口和实时重载端口号

```
ng serve --host 0.0.0.0 --port 4201 --live-reload-port 49153
```

## ng init

| 命令                               | 描述                                        |
| ---------------------------------- | ------------------------------------------- |
| `ng init <project-name> [options]` | 在当前所在目录下初始化一个新的 Angular 项目 |

| 参数             | 描述                                                 |
| ---------------- | ---------------------------------------------------- |
| `--dry-run` `-d` | 只输出要创建的文件和执行的操作，实际上并没有创建项目 |
| `--verbose` `-v` | 输出详细信息                                         |
| `--skip-npm`     | 在项目第一次创建时不执行任何npm命令                  |
| `--name`         | 指定创建项目的名称                                   |

## ng completion

| 命令            | 描述                                |
| --------------- | ----------------------------------- |
| `ng completion` | 将自动完成功能添加到ng命令的shell中 |

## ng doc

| 命令               | 描述                                      |
| ------------------ | ----------------------------------------- |
| `ng doc <keyword>` | 在浏览器中打开Angular文档并搜索当前关键字 |

## ng e2e

| 命令     | 描述                                       |
| -------- | ------------------------------------------ |
| `ng e2e` | 使用  `protractor` 在当前应用中运行e2e测试 |

## ng format

| 命令        | 描述                                    |
| ----------- | --------------------------------------- |
| `ng format` | 使用  `clang-format` 格式化当前项目代码 |

## ng generate

| 命令                           | 描述               |
| ------------------------------ | ------------------ |
| `ng generate <type> [options]` | 在项目中构建新代码 |
| `ng g <type> [options]`        | 简写               |

| 支持的类型 | 用法                              |
| ---------- | --------------------------------- |
| Component  | ng g component my-new-component   |
| Directive  | ng g directive my-new-directive   |
| Pipe       | ng g pipe my-new-pipe             |
| Service    | ng g service my-new-service       |
| Class      | ng g class my-new-class           |
| Interface  | ng g interface my-new-interface   |
| Enum       | ng g enum my-new-enum             |
| Module     | ng g module my-module             |
| Route      | ng g route my-route  `当前已禁用` |

构建的组件都会使用自用目录,除非  `--flat` 单独指定. 

| 参数                       | 描述                                              |
| -------------------------- | ------------------------------------------------- |
| `--flat`                   | 不在自用目录内创建代码                            |
| `--route=<route>`          | 指定父路由.仅用于生成组件和路由.默认为指定的路径. |
| `--skip-router-generation` | 跳过生成父路由配置。只能用于路由命令。            |
| `--default`                | 指定路由应为默认路由。                            |
| `--lazy`                   | 指定路由是延迟的。 默认为true。                   |

## ng get

| 命令                                        | 描述                    |
| ------------------------------------------- | ----------------------- |
| `ng get <path1, path2, ...pathN> [options]` | 从Angular CLI配置获取值 |

pathN是一个有效的JavaScript参数路径，例如“users[1].userName”。 如果未设置该值，将显示“undefined”。 此命令默认情况下仅在项目目录中工作。

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `--global` | 返回全局配置值，而不是本地配置值（如果都设置）. 此选项还可以使命令在项目目录外工作 |

## ng set

| 命令                                                         | 描述                      |
| ------------------------------------------------------------ | ------------------------- |
| `ng get <path1=value1, path2=value2, ...pathN=valueN> [options]` | 在Angular CLI配置中设置值 |

默认情况下，如果在项目内部运行，则设置项目配置中的值，如果不在项目内部，则失败。 pathN参数是一个有效的JavaScript路径，如“users [1] .userName”。 该值将被强制转换为正确的类型，或者如果类型无法强制，则会抛出错误。

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `--global` | 设置全局配置值，而不是本地配置值。 这也使  `ng set` 可以在项目之外工作。 |

## ng build

构建工件将存储在  `/dist` 目录中。 

ng build可以指定构建目标（--target = production或--target = development）和要与该构建一起使用的环境文件（--environment = dev或--environment = prod）。 默认情况下，使用开发构建目标和环境。

```
# 这是生产构建
ng build --target=production --environment=prod
ng build --prod --env=prod
ng build --prod

# 这是开发构建
ng build --target=development --environment=dev
ng build --dev --e=dev
ng build --dev
ng build
```

## ng github-pages:deploy

| 命令                               | 描述                                                   |
| ---------------------------------- | ------------------------------------------------------ |
| `ng github-pages:deploy [options]` | 构建生产应用程序，设置GitHub存储库，然后发布应用程序。 |

| 参数                       | 描述                                         |
| -------------------------- | -------------------------------------------- |
| `--message=<message>`      | 构建并提交信息.默认为 "new gh-pages version" |
| `--environment=<env>`      | angular 环境构建。 默认为“production”        |
| `--branch=<branch-name>`   | 推送页面的git分支。 默认为“gh-branch”        |
| `--skip-build`             | 在发布之前跳过构建项目                       |
| `--gh-token=<token>`       | 用于部署的API令牌,必须.                      |
| `--gh-username=<username>` | 使用的Github用户名,必须.                     |

## ng lint

| 命令      | 描述                         |
| --------- | ---------------------------- |
| `ng lint` | 在项目上运行codelyzer linter |

## ng test

| 命令                | 描述                       |
| ------------------- | -------------------------- |
| `ng test [options]` | 使用  `karma` 运行单元测试 |

| 参数                                                         | 描述                     |
| ------------------------------------------------------------ | ------------------------ |
| `--watch`                                                    | 继续运行测试. 默认为true |
| `--browsers` ,  `--colors` ,  `--reporters` ,  `--port` ,  `--log-level` | 这些参数直接传递给karma  |

## ng version

| 命令         | 描述                                 |
| ------------ | ------------------------------------ |
| `ng version` | 输出cli版本, node 版本和操作系统信息 |

| 参数      | 描述                     |
| --------- | ------------------------ |
| `--watch` | 继续运行测试. 默认为true |