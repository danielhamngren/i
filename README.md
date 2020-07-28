# i

## Compile

Run `cargo build`

## Running (during development)

Run `RUST_LOG=debug cargo run`

## Uploading files

Check the [client-side](client-side/) directory in this repo for some examples on how files or screenshots can be uploaded to the server.

### Using curl

Can be done using `curl`. The following command-line uploads a file `testfile.txt` in the current directory to the server.
A random filename will be generated by the server and returned in the JSON object, as well as in a `Location:` header (since the response will be a 303 See Other upon success). Thus, in the example below, the uploaded file will be available at `http://localhost:8088/Uake9Um7.txt`.

```
$ curl -F file=@testfile.txt -F options='{"useOriginalFilename":false}' http://localhost:8088

{"url":"http://localhost:8088/Uake9Um7.txt"}
```

The following example will upload the same file, but will use the original filename instead, which can be seen in the response URL.

```
$ curl -F file=@testfile.txt -F options='{"useOriginalFilename":true}' http://localhost:8088

{"url":"http://localhost:8088/testfile.txt"}
```

## Configuration

Set the following environmental variables to configure `i`.

* `AUTH_USER`: Set to the username for basic auth if you want to require authentication to upload files. Empty means no authentication.
* `AUTH_PASS`: Set to the password for basic auth if you want to require authentication to upload files. Empty means no authentication.
* `BASE_DIR`: Set to the file system directory where uploaded files will be stored to and served from. Default `./tmp`.
* `SERVER_URL`: Set to the complete server URL base which should be used when generating links. Default: `http://localhost:8088`.
* `PORT`: Which port `i` should listen to. Default `8088`.
