# Vault Secrets Buildkite Plugin

[![Build status](https://badge.buildkite.com/d5246cdaa0cb57cb86f0de499111ee4b4a00ef78941af6ba84.svg)](https://buildkite.com/elastic/vault-secrets-buildkite-plugin)

A simple buildkite plugin to map a Vault secret to a Step environment variable

## Requirements

`vault` and `jq` are expected to be installed on your Buildkite worker.

## Usage

Add the following to your `pipeline.yml`:

```yml
steps:
  - command: "<your-command>"
    plugins:
      - elastic/vault-secrets#v0.0.2:
          path: "secret/ci/elastic-<repo-name>/<secret-name>"
          field: "<secret-field-name>" # OPTIONAL
          env_var: "<environment-variable-mapping-secret>" # OPTIONAL
          path_depth: "2" # OPTIONAL
```

- `field` specifies the exact Vault secret field to retrieve.
  When `field` isn't defined, the entire secret is retrieved in json format
- `env_var` specifies the name of the environment variable that will contains the secret.
  When `env_var` the name of the environment variable will be based on the following format:
  `<UPPERCASE_SECRET_NAME>[_<UPPERCASE_FIELD_NAME>]_SECRET`
- `path_depth` specifies the number of elements of the path to use in the variable name when
  `env_var` isn't defined. When not defined the default value is `2`

Please refer to the test pipeline and scripts in ths `.buildkite` directory as examples.
