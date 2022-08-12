# Using Wiremock Proxy to Mock API Interaction

Writing unit tests using a third-party API can be a pain. Trying to mock out every aspect of the
APIs functionality to have a valid test can be tediously difficult. What if there were a way to
allow the API to execute normally, but feed it the results you want so your test to accurately test
your functionality?

The Wiremock testing framework provides not just a way to mock HTTP/s interaction with an API, but
can also intercept lives calls via proxy. This allows for configuring mock data to be returned to
the API without having to tediously mock out the objects required.

Let's construct an example to mock the Secrets Manager API requests in the AWS SDK. First we'll need
to complete some a one-time step, then we'll get into the code details.

## Generating the Certificate Authority

Wiremock requires a certificate authority that is capable of signing certificates. This involves
generating a certificate authority and adding the key signing capability. Without this capability
Wiremock will reject our custom certificate and revert to its own just-in-time generated certificate
authority.

We will use OpenSSL to generate our certificate. This software package is available on most, if
not all, Linux distributions, and on Mac. OpenSSL can be installed on Windows
[independently](https://wiki.openssl.org/index.php/Binaries) or Git for Windows comes with an
OpenSSL binary.

### Configuration

Generating a certificate authority requires some configuration up front. This configuration is
stored in a configuration file within the OpenSSL installation. However, we will need to make our
own copy to ensure the `keySign` capability is added to the certificate authority.

You can find an example configuration on [Github](https://www.github.com/) within the [example
project](https://www.github.com/. 
