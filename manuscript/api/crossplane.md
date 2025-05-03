# API (CRDs) & State Management (Controllers) With Crossplane

TODO: Intro

## Setup

> Watch [Nix for Everyone: Unleash Devbox for Simplified Development](https://youtu.be/WiFLtcBvGMU) if you are not familiar with Devbox. Alternatively, you can skip Devbox and install all the tools listed in `devbox.json` yourself.

> Skip executing `devbox shell` if you are already inside the Shell from one of the previous episodes.

```bash
devbox shell

source .env
```

> Watch [The Future of Shells with Nushell! Shell + Data + Programming Language](https://youtu.be/zoX_S6d-XU4) if you are not familiar with Nushell. Alternatively, you can inspect the `dot.nu` script and transform the instructions in it to Bash or ZShell if you prefer not to use that Nushell script.

```sh
./dot.nu setup idp_crossplane $HYPERSCALER

source .env
```

## Do

```sh
cat crossplane/repo.yaml

kubectl --namespace production apply --filename crossplane/repo.yaml

crossplane beta trace --namespace production githubclaim cncf-demo-app
```

> Wait until all the resources are `Available`.

```sh
git clone "https://github.com/$GITHUB_USER/cncf-demo-app"

cd cncf-demo-app

gh pr list

gh pr view init --json files

gh pr merge init --rebase

git pull

cat main.go

mkdir apps

cp ../crossplane/$HYPERSCALER-sql.yaml apps/silly-demo-db.yaml

cp ../crossplane/$HYPERSCALER-sql-password.yaml \
    apps/silly-demo-db-password.yaml

cat apps/silly-demo-db.yaml

cat apps/silly-demo-db-password.yaml

kubectl --namespace production apply \
    --filename apps/silly-demo-db-password.yaml

kubectl --namespace production apply \
    --filename apps/silly-demo-db.yaml

crossplane beta trace --namespace production \
    sqlclaim silly-demo-db

cp ../crossplane/app.yaml apps/silly-demo.yaml

cat apps/silly-demo.yaml

kubectl --namespace production apply \
    --filename apps/silly-demo.yaml

crossplane beta trace --namespace production \
    appclaim silly-demo
```

> Wait until all the resources are `Available`.

```sh
kubectl --namespace production get all,ingresses
```

> The Pod `STATUS` is `ErrImagePull` because there is no image. We'll fix that later.

```sh
kubectl --namespace production delete \
    --filename apps/silly-demo.yaml

git add .

git commit -m "Apps"

git push

cd ..
```

## Continue The Adventure

* [Policies](../policies-idp/README.md)
