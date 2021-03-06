# rating-api

Container exposes port 8080.
Required configuration via environment variables:

- MONGODB_URI:  `<set to mongoDB endpoint>`. The database is called `webratings` so the format would look like `mongodb://[endpoint]:27017/webratings`

Upon startup, the application checks if it can connect to the database. If the database is empty, it populates it with data.

## (Optional) MongoDB install in Kubernetes

```sh
# See Mongo DB Helm Chart (https://github.com/bitnami/charts/tree/master/bitnami/mongodb)

helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

helm install mongodb bitnami/mongodb \
    --set persistence.enabled=true \
    --set mongodbUsername=ratingsuser  \
    --set mongodbPassword=ratingspassword \
    --set mongodbDatabase=ratingsdb  \
    --set mongodbRootPassword=ratingspassword

MONGODB_URI="mongodb://ratingsuser:ratingspassword@mongodb:27017/ratingsdb"
```

## Helm install

```sh
helm upgrade --install rating-api ./rating-api \
    --set env.database_uri=$MONGODB_URI \
```

# Contributing



This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
