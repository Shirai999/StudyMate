#StudyMate — 学習ログ管理アプリ
##概要
 StudyMate は、毎日の学習内容を記録し、可視化し、継続をサポートする学習ログアプリです。
 学習時間・科目別ログ・達成度のグラフ化など、学習者が「習慣化」しやすい UI/UX を意識して設計しています。 
##主な機能
 ・学習科目ごとに学習ログを登録
 ・ダッシュボードで月ごとの統計を可視化 
 ・過去ログ検索
 ・ログイン / ログアウト機能
##使用技術
 バックエンド : Python 3.11 / Django 4.x
 フロントエンド : HTML / CSS / Bootstrap
 データベース : SQLite
 インフラ : AWS EC2（Amazon Linux 2023）
 アプリケーションサーバ : Gunicorn
 Wedサーバ : Apache（mod_proxyによるリバースプロキシ）
 
##システム構成図
 [Client] → [Apache] → [Gunicorn] → [Django] → [PostgreSQL]
 静的ファイル：Apache が /static/ を直接提供
 アプリ本体　：Apache → Gunicorn のプロキシ経由で Django を呼び出す
 
##デプロイ手順（概要）
 ※本番環境構築の再現ができるよう、実際に行った手順をまとめています。
 ###1. EC2 のセットアップ
    ・Amazon Linux 2023 インスタンス作成
    ・Python / pip / venv をセットアップ
    ・Django プロジェクトを GitHub から clone
###2. Gunicorn の設定
    ・gunicorn を venv にインストール
    ・systemd サービスファイルを作成し常時起動
###3. Apache の設定
　  ・mod_proxy を使って Gunicorn をリバースプロキシ
    ・/etc/httpd/conf.d/studymate.conf に VirtualHost を定義
    ・studymate.sock で Django と接続
###4. 静的ファイル
     python manage.py collectstatic  で出力した静的ファイルを Apache が配信

##画面イメージ
 ###1.[ログイン前のホーム画面]
 <img width="1919" height="965" alt="image" src="https://github.com/user-attachments/assets/2aaa20bc-b4f4-4540-afb2-f3c19224fc10" />
 ###2.[ログイン画面]
 <img width="1919" height="968" alt="image" src="https://github.com/user-attachments/assets/65bb2a0a-eb0a-4fef-bbab-d9aa15a4d652" />
 ###3.[ログイン後のホーム画面]
 <img width="1919" height="975" alt="image" src="https://github.com/user-attachments/assets/f4477ecd-c251-4b8d-907e-bab2ce7cbd52" />
 ###4.[学習ログ入力画面]
 <img width="1919" height="978" alt="image" src="https://github.com/user-attachments/assets/89ab5944-0ebc-4520-bc9c-ee226033d365" />
 <img width="1919" height="977" alt="image" src="https://github.com/user-attachments/assets/9cf40fd4-3012-42db-9077-189e7e95f40b" />
 <img width="1919" height="975" alt="image" src="https://github.com/user-attachments/assets/35e8db19-2140-42a1-84e7-b9c5ae1c8021" />
 ###5.[学習ログ一覧]
 <img width="1919" height="923" alt="image" src="https://github.com/user-attachments/assets/acb55554-7483-42d8-95c4-93fb38ab7205" />
 ###6.[ダッシュボード]
 <img width="1919" height="974" alt="image" src="https://github.com/user-attachments/assets/ebb84c73-0e28-416c-82c3-bbb09199b7af" />
 ###7.[Q&A掲示板]
 <img width="1919" height="936" alt="image" src="https://github.com/user-attachments/assets/bcaaccf4-4806-45ab-b4b3-533dd2afc7a3" />

##今後の改善予定
 ・HTTPS 化対応（Let’s Encrypt + Route53）
 ・モバイル最適化
 ・学習目標の自動リマインダー機能

##開発者
 Shirai
 学習ログ管理アプリの開発は大学の仲間と共同で行い、私はサーバ構築・バックエンド調整・AWSデプロイを中心に担当しました。  
 特に本番環境では、Amazon Linux 2023 上で Django + Gunicorn + Apache を構成し、単独でデプロイを行いました。


