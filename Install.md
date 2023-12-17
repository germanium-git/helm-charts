# Installation

## Step-by-step

### Create a public repository

### Create a branch called gh-pages.
Create a branch called gh-pages and push the file readme.md there. Do not merge the branch to main, it will be needed for the whole lifetime of the repository. The `index.yaml` will be pushed there each time when a new release is created to keep track of all the previous releases.

### Pages
Let’s follow the Chart Repository Guide to make sure our repo is ready for hosting the Helm Chart Repo. You’ll want to make sure your gh-pages branch is set as GitHub Pages. Click on your repo Settings, scroll down to GitHub pages section, and set as per below:

![](/pictures/gh-pages.png)

The content of the readme.md from the gh-branch is shown up when the page is open.

### GH Action Chart Releaser

Create a GH Action according to the instruction at https://helm.sh/docs/howto/chart_releaser_action/.

Save the release.yaml to .github/workflows/release.yaml to the main branch.

Don't get confused by secrets.GITHUB_TOKEN used in the action. It's created automatically when enabling the option "Workflows have read and write permissions in the repository for all scopes". Do not create any additional secrets.

Repository > Settings > Actions > General > Workflow permissions > Read and Write permissions

Bear in mind that the secret GITHUB_TOKEN is not shown in the Repository > Settings > Secrets and variables.

Without this option being enabled the run of the action ends up with the error "permission denied to github-actions[bot]" which can be solved by:
https://stackoverflow.com/questions/72851548/permission-denied-to-github-actionsbot

Alternatively, if you don’t want to grant the github-actions[bot] account permission to push directly to the repository, you can use a personal access token (PAT) with the necessary permissions instead. More information in the article:

https://medium.com/@eduardo854/creating-an-exclusive-helm-repository-using-github-pages-9caa57c1b58f



### CNAME (optional)

Create a CNAME `helm.germanium.cz` record in your DNS provider for `germanium-git.github.io`.


## Test Chart

Create a simple helm chart to demonstrate the repository works as expected and each new version is packaged and released.

https://helm.sh/docs/chart_template_guide/getting_started/

```
cd charts

# Create a simple chart called testchart
helm create testhart

# Remove all unnecessary files
rm -rf testchart/templates/*

# Create a template for a simple configmap
cat << EOF > testchart/templates/configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  value: "Hello World"
EOF
```

Push the changes to the master and chcek if the GH Actions are triggered and a new release is created.