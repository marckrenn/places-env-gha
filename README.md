# places-env-gha

This is the companion Github Action to [_places-env_](https://github.com/marckrenn/places-env). _places-env-gha_ installs _places-env_, injects crypto keys and generates environment files so that they can be used downstream.

## Usage

1. **Add Checkout:**
    
    To your workflow, before running _places-env-gha_

    ```yaml
    - uses: actions/checkout@v3
    ```

2. **Add _places-env-gha_**

    For example:
    ```yaml
    - name: places-env
        uses: marckrenn/places-env-gha@v1.0.1
        with:
          version: "latest" # Installs latest version of places-env
          keys: |
            prod: ${{ secrets.PROD_KEY }} # Injects prod crypto key from secrets; creates file prod in .places/keys/
          generate: prod # Generates prod environment file according to places.yaml (.env.prod)
    ```

## Documentation

```yaml
- name: places-env
    uses: marckrenn/places-env-gha@v1.0.1 # Use >=1.0.1!
    with:
```
| Property | Type | Default | Required | Description | Examples |
|----------|------|---------|:--------:|-------------|----------|
| `version` | `String` | `"latest"` | ❌ | Specifies _places-env_ version to install. This can either be `"latest"` or a semantic version | Examples[^1] |
| `keys` | `Block-list KV` | `""` | ❌ | Dictionary of key (filename) value (crypto key). These keys will be injected into `.places/keys`. **Note:** Must be in the exact format as the provided examples | Example[^2] |
| `generate` | `String or Block-List` | `""` | ❌ | Environment (files) to generate | Examples[^3]|
| `generate-all` | `Bool` | `""` | ❌ | Generates all environment files specified in [`places.yaml`](https://github.com/marckrenn/places-env/tree/main?tab=readme-ov-file#placesyaml) | `generate-all: true` |


[^1]: `version` examples:

    Install latest version of _places-env_:
    ```yaml
    version: "latest"
    ```

    Install specific version of _places-env_:
    ```yaml
    version: "==1.0.3"
    ```

[^2]: `keys` example:

    Inject one or more crypto keys:
    ```yaml
    keys: |
        prod: ${{ secrets.PROD_KEY }}
        dev: ${{ secrets.DEV_KEY }}
    ```

[^3]: `generate` examples:

    Generate a single environment file:
    ```yaml
    generate: prod
    ```

    Generate multiple environment files:
    ```yaml
    generate: |
        - prod
        - dev
    ```


## Example / Demo

Please refer to [_places-env-example_](https://github.com/marckrenn/places-env-example) and explicitly to [its example workflow](https://github.com/marckrenn/places-env-example/blob/develop/.github/workflows/places-env.yaml).

