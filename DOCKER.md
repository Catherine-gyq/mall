# Docker 运行（本仓库一键启动）

下面配置可在项目根目录直接运行 `docker compose up -d --build`，会自动启动：

- 基础环境：MySQL、Redis、RabbitMQ、MongoDB、Elasticsearch、MinIO
- 应用：`mall-admin`、`mall-search`、`mall-portal`

## 1. 前置条件

- 已安装 Docker Desktop / Docker Engine
- `docker compose` 可用

## 2. 启动

在项目根目录执行：

```bash
docker compose up -d --build
```

首次构建会在镜像构建阶段执行 Maven 下载依赖，时间较长属正常现象。

## 3. 访问地址（默认端口）

- `mall-admin`：`http://localhost:8080`
- `mall-search`：`http://localhost:8081`
- `mall-portal`：`http://localhost:8085`
- RabbitMQ 管理台：`http://localhost:15672`（账号/密码：`mall`/`mall`）
- MinIO Console：`http://localhost:9001`（账号/密码：`minioadmin`/`minioadmin`）

## 4. 数据库初始化

`docker-compose.yml` 已挂载 `document/sql/mall.sql` 到 MySQL 的初始化目录，首次启动并创建数据卷时会自动导入。

如果你之前已经启动过（数据卷已存在）但没导入成功，可先清理数据卷后再启动：

```bash
docker compose down -v
docker compose up -d --build
```

## 5. 常见问题

- Linux 上启动 Elasticsearch 可能需要设置 `vm.max_map_count=262144`（Docker Desktop 一般不需要）。

