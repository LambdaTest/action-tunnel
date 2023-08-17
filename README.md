![LAMBDATEST Logo](https://www.lambdatest.com/resources/images/logos/logo.svg)
# LambdaTest Tunnel Action

[![Test](https://github.com/LambdaTest/LambdaTest-tunnel-action/actions/workflows/main.yml/badge.svg?branch=master&event=push)](https://github.com/LambdaTest/LambdaTest-tunnel-action/actions/workflows/main.yml)

[![Releases](https://github.com/LambdaTest/LambdaTest-tunnel-action/actions/workflows/update_semver.yml/badge.svg)](https://github.com/LambdaTest/LambdaTest-tunnel-action/actions/workflows/update_semver.yml)

This action seamlessly integrates LambdaTest Tunnel and
run Selenium tests on 2000+ browsers for your locally hosted or
privately hosted pages with LambdaTest Selenium Grid.

## Example usage

```yaml
jobs:
    test-tunnel:
        runs-on: ubuntu-latest
        steps:
            # ...
            -name: Start Tunnel
             uses: LambdaTest/LambdaTest-tunnel-action@v2
             id: tunnel
             with:
               user: ${{ secrets.LT_USERNAME }}
               accessKey: ${{ secrets.LT_ACCESS_KEY }}
               tunnelName: "testTunnel"
            - run: npm test
            - name: Export Tunnel Logs for debugging
              uses: actions/upload-artifact@v2
              with:
                name: tunnel_logs
                path: ${{ steps.tunnel.outputs.logFileName }}
            # ...
```

## Inputs

### `user`

**Required** LambdaTest user email.

### `accessKey`

**Required** LambdaTest user Access Key.
> We suggest using [github secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) for storing LambdaTest access key

### `tunnelName`

**Required** Tunnel name to uniquely identify your tunnel on LambdaTest platform.

### `proxyHost`

Proxy host if connecting tunnel via proxy.

### `proxyPort`

Proxy port if connecting tunnel via proxy.

### `proxyUser`

Proxy username if connecting tunnel via proxy that has authentication enabled.

### `proxyPass`

Proxy password if connecting tunnel via proxy that has authentication enabled.

### `sharedTunnel`

Sharing tunnel among team members.

### `ingressOnly`

Routes only incoming traffic via the proxy specified.

### `egressOnly`

Routes only outgoing traffic via the proxy specified.

### `mitm`

Enable Man in the Middle Mode

### `dns`

Comma separated list of dns servers.

### `verbose`

Run tunnel in verbose mode.

### `loadBalanced`

Run tunnel in load balanced mode.

### `bypassHosts`

Comma separated list of host to bypass from tunnel.

### `basicAuth`

Add basicAuth to provided hosts on the format "https://USER:PWD@YourWebsite.com"
> We suggest using [github secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets)
for sensitive information

## Outputs

### `port`

Port on which tunnel api server is running.

### `logFileName`

Name of log file of tunnel.

