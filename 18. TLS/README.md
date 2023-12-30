Restrict communication between `etcd` and `api server` to the cipher `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256` and also restrict the `api server` minimum TLS version to `TLS 1.2`

1. Edit the `API server` manifest and add the following two arguments

    ```
    --tls-min-version=VersionTLS12
    --tls-cipher-suites=TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    ```

1. Edit the `etcd` manifest and add the following argument

    ```
    --cipher-suites=TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    ```

1. Wait for both pods to restart. This may take a minute or more.