# sonarcloud-project-config

Make and/or configure the Sonarcloud projects automatically to use cloud or
CI driven analysis.

## Usage

### Inputs

- `create-missing-project`: If `true` creates a sonarcloud project if not present. [**optional, default:** `true`]
- `sonarcloud-org`: If set, is the sonarcloud org to use instead of the github org/owner.  [**optional, default:** ``]
- `analysis-mode`: If `ci` the analysis mode is set to CI driven.  If `cloud` the
   analysis mode is set to Cloud driven.  Otherwise the value is not changed. [**optional, default:** `unchanged`]
- `new-code-delta`: Set the way new code is identified to one of: "", `previous_version`, `date`, `days`, `tag` [**optional, default:** `""`]
- `new-code-tag`: If `new-code-delta` is set to `tag` this field specifies the tag to diff against.
- `new-code-date`: If `new-code-delta` is set to `date` this field specifies the date to measure from.
- `new-code-days`: If `new-code-delta` is set to `days` this field specifies the number of days.
- `sonar-token`: The SONAR_TOKEN used to access/upload to sonarcloud. [**required**]

### Outputs

- None

### Example workflow

```yaml
name: Test And Upload
on: push

jobs:
    package_rpm:
        runs-on: [ ubuntu-latest ]
        steps:
        - uses: actions/checkout@v3

        - run: echo "test things"

        - uses: xmidt-org/sonarcloud-project-config@v1
          with:
            create-missing-project: true
            analysis-mode: ci
            new-code-delta: commit
            sonar-token: ${{ secrets.SONAR_TOKEN }}
```

In this example the new project is created if needed and set to CI based analysis,
with the new code being defined as the previous version.

## Contribute

See [this file](CONTRIBUTING.md) for details.

## License

This project is released under the [Apache 2.0 license](LICENSE).
