# regex-action

A GitHub action that applies a regular expression to an input and outputs the groups.

## Inputs

| Name | Description | Required |
| --- | --- | --- |
| `regex` | The regular expression | `true` |
| `ref` | What to apply the regex to | `true` |

## Example

```yaml
jobs:
  decipher:
    name: Decipher
    runs-on: ubuntu-latest
    steps:

      - name: Parser
        id: parser
        uses: johngeorgewright/regex-action@v2.0.0
        with:
          ref: refs/heads/master
          regex: ^refs/tags/(?P<package>[a-zA-Z0-9_-]+)-v(?P<version>\d+.\d+.\d+)$

      - name: Debug
        run: |
          echo 'package = ${{ fromJSON(steps.parser.outputs.groups).package }}'
          echo 'version = ${{ fromJSON(steps.parser.outputs.groups).version }}'
