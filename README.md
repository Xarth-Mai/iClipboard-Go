<div align="center">
  <img src="/images/clipboard-icon.png" style="display: inline-block; vertical-align: middle;">
  <h1 style="display: inline-block; vertical-align: middle;">iClipboard-Go It's MyGO!!!!!</h1>
</div>

![GitHub release (latest by date)](https://img.shields.io/github/v/release/Xarth-Mai/iClipboard-Go)

iClipboard-Go is an application to share cilpboard between 💻Linux and 📱iOS

## Usage

### For iOS users

4. Have fun...😊

## Configuration

`iClipboard-Go` will create two file which are `config.json` and `log.txt` in the execute path when first running

You can make customization by editing `config.json`

### `config.json`

- `port`
  - type: `string`
  - default: `"8086"`

- `logLevel`
  - type: `string`
  - default: `"warning"`
  - values: `"panic"`, `"fatal"`, `"error"`, `"warning"`, `"info"`, `"debug"`, `"trace"`

- `authkey`
  - type: `string`
  - default: `''`

- `authkeyExpiredTimeout`
  - type: `int64`
  - default: `30`

- `tempDir`
  - type: `string`
  - default: `./temp`

- `reserveHistory`
  - type: `Boolean`
  - default: `false`

- `notify`
  - type: `object`
  - children:
    - `copy`
      - type: `Bollean`
      - default: `false`
    - `paste`
      - type: `Boolean`
      - default: `false`

## API

The default http server will listen `8086` port and you can't chanage that since hardcoded.

### Common headers

#### Required

- `X-API-Version`: indicates version of api

#### Optional

- `X-Client-Name`: indicates name of device
- `X-Auth`: hashed authkey. Value from `md5(config.authkey + timestamp/30)`

### 1. Get windows clipboard

> Request

- URL: `/`
- Method: `GET`

> Reponse

- Body: `json`

```json
// 200 ok

{
  "type": "text",
  "data": "clipboard text on the server"
}

{
  "type": "file",
  "data": [
    {
      "name": "filename",
      "content": "base64 string of file bytes"
    }
    ...
  ]
}

```

### 2. Set windows clipboard

> Request

- URL: `/`
- Method: `POST`
- Headers:
  - `X-Content-Type`: indicates type of request body content
    - `required`
    - values: `text`, `file`, `media`

- Body: `json`

For text:

```json
{
  "data": "text you want to set"
}
```

For file:

```json
{
  "data": [
    {
      "name": "filename",
      "base64": "base64 string of file bytes"
    }
  ]
}
```

> Reponse

Reponse body is empty. If set successfully, status code will be `200`
