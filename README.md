1. Run `./test/service/run_ssl_server.sh`. This builds and runs
   test service on port `443`. Self-signed certificate would be placed
   in the `./test/service/build/` directory by the script.

2. Run `./test/service/run_ssl_client.sh`. This basically runs
   `openjdk11-cacert-import` image with `test IP_ADDRESS` arguments
   and `./test/service/build/` directory mounted:

```
docker run  \
    -v "$(pwd)"/test/service/build:/usr/local/share/ca-certificates \
    091468197733.dkr.ecr.us-east-1.amazonaws.com/java:openjdk11-cacert-import \
    test IP_ADDRESS
```
where `IP_ADDRESS` is this notebook interface address.

Note: do not use `localhost` above, only the IP address of net interface,
as host's `localhost` is not accessible from a container.

If it prints
```html
<html><body><h1>It works!</h1></body></html>
```
then it works.

3. Kill SSL service with `docker kill ssltest_service`.
