```bash
# 一番初めのコンテナ立ち上げ
docker compose up -d

# 立ち上がり確認
# もしpostgresqlのコンテナが立ち上がらない場合は、logsとdataディレクトリの中身を空にする
docker ps

# コンテナに入る
docker exec -it コンテナ名 bash

# プロジェクト作成(laravel11を指定し、srcディレクトリに作成)
composer create-project "laravel/laravel=11.*" src

# webコンテナとnginxコンテナのvolumesの./の後にsrcを追加する
# コードはlaravelEnvのブランチ名「After_create_project」

# srcを追加して書き換えてファイルを表示させる
# これでlaravelのページが表示される
docker compsoe up -d
```

【DB接続確認】

```bash
# resources/views/welcome.blade.phpのfooterの上に記述
<?php
	try {
		\DB::connection()->getPDO();
		echo \DB::connection()->getDatabaseName(); # DBに接続できている場合、DB名が表示される
	} catch (\Exception $e) {
		echo 'None'; # 接続できていない場合は、Noneと表示される
	}
	
	phpinfo(); # phpの情報を表示
?>
```

localhost:8080にアクセスして、sessionsテーブルが無いとエラーになったら以下のコマンドを実行

```bash
php artisan migrate
```
