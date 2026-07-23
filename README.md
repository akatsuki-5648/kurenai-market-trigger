# 紅月市場MS Layer3: 外部トリガー

`izumoitachi-gif/discord-rss-notifier` の workflow群が GitHub Actions schedule cron 側で詰まった時の**外部発火冗長経路**。

## 構造

- **cron**: 5分毎 (1,16,31,46分・他Bot衝突ゼロ時刻)
- **中身**: discord-rss-notifier の7 workflow を dispatch API で叩くだけ
- **必要Secret**: `CROSS_REPO_PAT` = discord-rss-notifier に workflow_dispatch 権限あるPAT

## 設計思想

パパ設計「フックはどこでどう増やしてもよい、結果は同じ、ルートが増える」の実装。
現discord-rss-notifierとは**完全分離した別リポ・別schedule登録**なので、
現リポの詰まりに巻き込まれない冗長経路になる。

参照: `.claude/中期記憶/Discord/金融市場Bot_パットンMS_20260716/08_発火経路多重化_パパ設計.md` Layer3
