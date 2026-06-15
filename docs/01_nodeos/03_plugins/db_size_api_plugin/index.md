## Description

The `db_size_api_plugin` retrieves analytics about the blockchain.

* free_bytes
* used_bytes
* reclaimable_bytes
* size
* indices

<!--
## Usage

```console
# Not available
```
-->

## Options

None

## Dependencies

* [`chain_plugin`](../chain_plugin/index.md)
* [`http_plugin`](../http_plugin/index.md)

### Load Dependency Examples

```console
# config.ini
plugin = vexcore::chain_plugin
[options]
plugin = vexcore::http_plugin
[options]
```
```sh
# command-line
nodeos ... --plugin vexcore::chain_plugin [operations] [options]  \
           --plugin vexcore::http_plugin [options]
```
