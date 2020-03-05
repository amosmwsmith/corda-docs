+++
date = "2020-01-08T09:59:25Z"
title = "Enclave storage"
aliases = [ "/releases/4.1/design/sgx-infrastructure/details/enclave-storage.html",]
menu = [ "corda-enterprise-4-1",]
tags = [ "enclave", "storage",]
+++


# Enclave storage

The enclave storage is a simple static content server. It should allow uploading of and serving of enclave images based
            on their measurement. We may also want to store metadata about the enclave build itself (e.g. github link/commit hash).

We may need to extend its responsibilities to serve other SGX related static content such as whitelisting signatures
            over measurements.

