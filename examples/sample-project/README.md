# Sample project

Lockfiles for trying the scan command without using your own code.

```sh
cd examples/sample-project
osv-scanner scan source -r --offline --download-offline-databases --all-packages --format cyclonedx-1-5 . \
  | jq '{bomFormat,components:[.components[]|select(.purl)|{purl}]}'
```

The output is the JSON that Meerkat would receive.
