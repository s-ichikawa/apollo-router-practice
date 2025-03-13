[apollo router](https://www.apollographql.com/docs/graphos/routing)を試すための練習用

サブグラフはgqlgenで作成しています

# 必要なもの

[rover](https://www.apollographql.com/docs/rover/commands/supergraphs#supergraph-compose)
サブグラフのSchemaからスーパーグラフのSchemaを生成するのに必要

[apollo router](https://www.apollographql.com/docs/graphos/reference/router/self-hosted-install)
```shell
curl -sSL https://router.apollo.dev/download/nix/latest | sh && mv router ./bin/router
```

# 動かし方

## サブグラフを起動する

accountグラフを起動
```shell
cd subgraphs/account && go run ./server.go
```

todoグラフを起動
```shell
cd subgraphs/todo && go run ./server.go
```

## スーパーグラフを起動する
Schemaに変更がある場合はスーパーグラフのSchemaを更新する
```shell
rover supergraph compose --config codegen.yml > federated-schema.graphqls
```
apollo routerを起動
```shell
./bin/router --dev --supergraph federated-schema.graphqls
```