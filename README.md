# Flovia-Sample
This repo for flovia sample code

## MCPサーバーの設定例

> 設定後は認証する必要があります！

```json
{
  "mcpServers": {
    "flovia": {
      "type": "http",
      "url": "https://api.flovia.dev/mcp"
    }
  }
}
```

## 利用可能なMCPサーバーのツール

```bash
データ取得（読み取り専用）

┌──────────────────┬───────────────────────────────────────────────────────────────────────────────────────┐
│      ツール      │                                       主な用途                                        │
├──────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_nansen    │ ウォレットのラベル、スマートマネー、トークン保有者、トークンフロー、Perps、Polymarket │
├──────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_coingecko │ 価格、時価総額、チャート、OHLC、DEXプール                                             │
├──────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_quicknode │ EVMチェーン上のトランザクション結果、残高、コントラクトの読み取り、イベントログ       │
├──────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_zerion    │ 公開ウォレットのポートフォリオ、トークンのポジション、デコード済みトランザクション    │
├──────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_exa       │ Web検索（公開ソース、ドキュメント、引用付きの抜粋）                                   │
├──────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_firecrawl │ 公開されているHTMLページ1つをMarkdownに変換                                           │
└──────────────────┴───────────────────────────────────────────────────────────────────────────────────────┘

補助

┌──────────────────┬────────────────────────────────────────────────────────────────────────────────────────────┐
│      ツール      │                                            用途                                            │
├──────────────────┼────────────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_endpoints │ Nansenで使うエンドポイントを質問内容から選ぶ                                               │
├──────────────────┼────────────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_lookup    │ 過去のルックアップを参照する                                                               │
├──────────────────┼────────────────────────────────────────────────────────────────────────────────────────────┤
│ flovia_openai    │ 取得したデータをもとに要約やレポートを作る（任意）。生成した文章は市場の根拠にはなりません │
└──────────────────┴────────────────────────────────────────────────────────────────────────────────────────────┘

アカウント・管理

┌──────────────────────────────────────────┬────────────────────────────────────────┐
│                  ツール                  │                  用途                  │
├──────────────────────────────────────────┼────────────────────────────────────────┤
│ flovia_status                            │ 接続とアカウントの状態                 │
├──────────────────────────────────────────┼────────────────────────────────────────┤
│ flovia_usage_today                       │ 今日の利用状況                         │
├──────────────────────────────────────────┼────────────────────────────────────────┤
│ flovia_data_consent                      │ データ共有の同意設定                   │
├──────────────────────────────────────────┼────────────────────────────────────────┤
│ flovia_feedback / flovia_feedback_status │ フィードバックの送信と、その状況の確認 │
└──────────────────────────────────────────┴────────────────────────────────────────┘

使い方を補足します。

- ツール名を指定する必要はありません。質問の内容に合わせて、適したツールを選びます。
- 無料枠では、1回に1件ずつ順番にルックアップします。

最初の質問どおり flovia_status で接続状態を確認したい場合や、試してみたい質問がある場合は教えてください。
```

## プロンプト例

```bash
Call Flovia's flovia_status once and summarize the result. If it includes stopped or free_pending, tell me what they say. Don't call any other Flovia tools. If Flovia's tools aren't available, run only your app's MCP list command (for example claude mcp list or codex mcp list; in Cursor, look at MCP settings) and tell me which of these it shows, with its fix: flovia not listed → add it again from Quick Install in Flovia Console; needs sign-in, 401 or unauthorized → sign in to Flovia again in the app (Claude Code: /mcp, Codex: codex mcp login flovia). Never show, read out, or paste a token or any header value, and don't edit settings.
```

```bash
Who are the top holders of USDC on Ethereum (contract 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48)? Tell me which data source you used.
```

```bash

┌─────┬────────────────────────────────────────────┬───────────────────┬───────────┬──────────────┐
│  #  │                  Address                   │   Nansen label    │ USDC held │ 7-day change │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 1   │ 0x37305b1cd40574e4c5ce33f8e8306be057fd7341 │ Token Billionaire │ 4.169B    │ +158.1M      │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 2   │ 0xe1940f578743367f38d3f25c2d2d32d6636929b6 │ Token Billionaire │ 1.700B    │ 0            │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 3   │ 0xffa69c0080582098af595156240214b742735a5e │ Token Billionaire │ 1.583B    │ 0            │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 4   │ 0xad354cfbaa4a8572dd6df021514a3931a8329ef5 │ Token Billionaire │ 1.400B    │ 0            │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 5   │ 0xee7ae85f2fe2239e27d9c1e23fffe168d63b4055 │ Token Millionaire │ 1.123B    │ +473.3M      │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 6   │ 0x40ec5b33f54e0e8a33a975908c5ba1c14e5bbbdf │ Token Contract    │ 1.025B    │ +13.7M       │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 7   │ 0x3b4d794a66304f130a4db8f2551b0070dfcf5ca7 │ lighter.eth       │ 583.0M    │ −7.1M        │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 8   │ 0x36db199f0a1cd131ad0b5cf4fe94286faab9fda5 │ Token Millionaire │ 523.9M    │ −17.8M       │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 9   │ 0x08f619716db7c6245401b543e59acac1d25cb483 │ Token Millionaire │ 502.8M    │ 0            │
├─────┼────────────────────────────────────────────┼───────────────────┼───────────┼──────────────┤
│ 10  │ 0xe20d20b0cc4e44cd23d5b0488d5250a9ac426875 │ Token Millionaire │ 500.0M    │ 0            │
└─────┴────────────────────────────────────────────┴───────────────────┴───────────┴──────────────┘

The data was retrieved at 2026-10-24 03:23 UTC. Nansen gives the dollar value of each row at about $1 per USDC.

What the numbers show
- My sum of the top 10 is about 13.11B USDC.
- Nansen reported a share of supply of 0.0 for every address, which can't be right for wallets this large. I left that column out, so I can't tell you what fraction of USDC supply these wallets hold.

Caveats
- Most labels don't say who owns the wallet. "Token Billionaire" and "Token Millionaire" are just size labels. #6 is a smart contract, so its balance probably belongs to many users. "lighter.eth" is a name, and a name alone doesn't prove what the address is.
- Labels can't be trusted on their own. Anyone can create names like these, so I'm only reporting what Nansen returned, not checking it.
- These are separate addresses, not separate people. One company or person could own several of them.
- This is only page 1. The ranking continues past #10, and this list doesn't show how USDC is spread across all holders.

Data provided by Nansen

Possible next steps:
1. Where this token's money has been flowing (uses some of this week's free use)
2. This token's price chart for the same period (uses some of this week's free use)
```

## 参考文献
- [開発者コンソール](https://console.flovia.dev/groupbuy/)
