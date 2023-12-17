# Helm-charts

## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

```
helm repo add germanium-git https://germanium-git.github.io/helm-charts
```

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo germanium-git` to see the charts.

To install the my-\<chart-name> chart:

    helm install my-<chart-name> germanium-git/<chart-name>

To uninstall the chart:

    helm delete my-<chart-name>

## Page

The page with the instructions on how to use the helm repository is available on the following two addresses:

https://helm.germanium.cz/

https://germanium-git.github.io/helm-charts/