# tenancy
stancl/tenancy動かしてみる

## 初回起動時

**データベース作成**

```bash
# mysqlコンテナにログイン
$ docker exec -it db-host bash
```

```bash
# mysqlにログイン
$ mysql -u root -p
(pass: root)
```

```sql
-- データベース作成
CREATE DATABASE IF NOT EXISTS tenancy;
-- ユーザの作成
CREATE USER IF NOT EXISTS 'tenancy'@'%' IDENTIFIED BY 'password';
-- ユーザへの権限付与
GRANT ALL PRIVILEGES ON *.* TO 'tenancy'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

**マイグレーション実行**

```bash
# phpコンテナにログイン
$ docker-compose exec php bash

# マイグレーション実行
$ php artisan migrate
```

# メモ

## stancl/tenancyのインストール

```bash
$ composer require stancl/tenancy
```

## tenancyの自動設定

stancl/tenancyをインストール後、利用するためのコード追加や更新作業を自動で行う

```bash
$ php artisan tenancy:install

Installing stancl/tenancy...
✔️  Created config/tenancy.php
✔️  Created routes/tenant.php
✔️  Created TenancyServiceProvider.php
✔️  Created migrations. Remember to run [php artisan migrate]!
✔️  Created database/migrations/tenant folder.
✨️ stancl/tenancy installed successfully.
```
