# gitでのリモートとローカルのやりとりを図にしてみた
## 機能ブランチの元となるブランチの最新を取得
### 新たにクローンする

```bash
git clone -b <ブランチ名> <リポジトリのURL> <保存先フォルダ名>
```

```mermaid
flowchart LR

subgraph "Remote Repository (origin)"
    RM["main"]
end

subgraph Local
    subgraph Remote Tracking
        RT["origin/main"]
    end
    subgraph Local Repository
        LC["main"]
    end
end

RM ---- RT
RT ---- LC
```
### 既にローカルに存在するレポジトリを最新の状態に追従する
```bash
git fetch
git merge
or
git pull
```

```mermaid
flowchart LR

subgraph "Remote Repository (origin)"
    RM["main"]
end

subgraph Local
    subgraph Remote Tracking
        RT["origin/main"]
    end
    subgraph Local Repository
        LC["main"]
    end
end

RM -- git fetch --> RT
RT -- git merge / git pull --> LC
```

## 機能ブランチをローカルに作成
```bash
git switch -c <機能ブランチ名>
```

```mermaid
flowchart LR

subgraph "Remote Repository (origin)"
    RM["main"]
end

subgraph Local
    subgraph Remote Tracking
        TM["origin/main"]
    end
    subgraph Local Repository
        LM["main"]
        LB["future_branch_1"]
    end
end

RM ---- TM
TM ---- LM
```

+ ローカルにブランチを作成しただけで、リモート側はなにも変更していない
  + つまり、新しく作成した機能ブランチは、リモート追跡と紐づいていない

## ローカル機能ブランチでの修正をコミット＆プッシュ

```mermaid
flowchart LR

subgraph "Remote Repository (origin)"
    RM["main"]
    RB["future_branch_1"]
end

subgraph Local
    subgraph Remote Tracking
        TM["origin/main"]
        TB["origin/future_branch_1"]
    end
    subgraph Local Repository
        LM["main"]
        LB["future_branch_1"]
    end
end

RB ---- TB
TB ---- LB
```

## GitHub上で機能ブランチから上流ブランチにプルリクエスト

```mermaid
flowchart

subgraph "Remote Repository (origin)"
    RM["main"]
    RB["future_branch_1"]
end

RB -- pull request --> RM

```