
# Intro
Helm is not currently able to pull dependent charts from Quay. You will need to use the Helm plugin `appr-helm-plugin` to use quay. This plugin operates outside of the standard Helm set of verbs, so there is an additional workflow you must observe. 

Reference: No support for Helm Requirements #3  https://github.com/app-registry/appr-helm-plugin/issues/3

# In your requirements.yaml file, add a reference to your the Quay chart on which you want to depend. Use this format (which is only recognized by the appr-helm-plugin):
```
appr:
  - name: quay.coredev.cloud/<quay-username-or-company>/<quay-application-name>
    repository: appr://
    version: <version-number>
```

# Invoke the appr-helm-plugin. The plugin will perform the following operations:
    1. Download packages from the app-registry server into a local folder <chart-folder>/appr_folder
    2. Overwrite your `appr:` section that you added to the requirements.yaml file. This overwrite will add a section referencing the downloaded local copy of the chart from Quay

cd <chart-folder>
helm registry dep --overwrite

# Invoke a standard Helm depency update. This will perform the following operations:
	1. Download all of the dependencies in the standard `dependencies:` section of your requiremetns.yaml file, placing them in the <chart-folder>/charts folder as usual
	2. Copy the charts from <chart-folder>/appr_folder into <chart-folder>/charts 

cd <project-folder>
helm dependency update <chart-folder>


# Install as usual
helm install <chart-folder> [--namespace <namespace-name>]


# Push to quay
cd <chart-folder>
	