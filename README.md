# port-range-merger

Collapse overlapping or adjacent port ranges into a minimal equivalent list.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "ranges": [
    [
      80,
      81
    ],
    [
      82,
      83
    ],
    [
      443,
      443
    ],
    [
      80,
      80
    ]
  ]
}
```

Result:

```json
{
  "ranges": [
    [
      80,
      83
    ],
    [
      443,
      443
    ]
  ]
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Merge only ranges with the same protocol, direction, and policy action.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [route-longest-prefix](https://github.com/sal-s-root/route-longest-prefix), [syslog-severity-summary](https://github.com/sal-s-root/syslog-severity-summary).
