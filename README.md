# Gitleaks

Thanks to [Zachary Rice](https://github.com/zricethezav) for creating and maintaining gitleaks.
Thanks to [Jesse Houwing](https://github.com/jessehouwing) for providing a gitleaks config that has most of Microsoft's deprecated credscan rules ported to it.

This Azure DevOps task downloads and runs a basic gitleak scan on the specified location. It can only scan already checked-out repo's on the agent because it is currently not possible to scan Azure DevOps repo-urls. See [this github issue](https://github.com/zricethezav/gitleaks/issues/440) for more information.

## YAML Snippet

```yaml
# Run Gitleaks on Source Repository
- task: Gitleaks@1
  inputs:
    version: 'latest'
    scanfolder: '$(Build.SourcesDirectory)'
    configtype: 'predefined'
    predefinedconfigfile: 'gitleaks.toml'
    verbose: true
```

## Arguments

| Name | Description |
|-|-|
| version |  Version of Gitleaks to be used. Use Semver. Set to latest to download the latest version of gitleaks |
| scanfolder | The location to be scanned. Defaults to $(Build.SourcesDirectory). This is passed to gitleaks as '--path=' |
| configtype | Can be 'default', 'predefined', 'custom'. When set to 'predefined' you can pass the argument 'predefinedconfigfile. When set to 'custom' you need to provide 'configfile' with the location of your gitleaks toml file |
| predefinedconfigfile | When set to 'UDMSecretChecks.toml' it uses the Credscan config file provided by Jesse Houwing |
| configFile | Sets the custom configfile in your repo. Use a relative path: '.github/gitleaks.config' |
| verbose | When set to true, gitleaks prints verbose output |
| nogit |  When set to true, gitleaks will be executed with the --no-git option |
| uploadresults | When set to true, the results of gitleaks (in JSON) will be uploaded as an artifact |