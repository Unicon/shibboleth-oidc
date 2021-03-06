# shibboleth-oidc
OpenIDConnect support for the Shibboleth Identity Provider version 3

## Scope
We are working on adding support for the OpenID Connect protocol to the Shibboleth Identity Provider v3. Realistically, these
are the items we are planning to address:

* Authorization code workflow
* Administration and registration of OIDC RPs with the IdP. 
* Ability to resolve, consume and release OIDC claims, taking advantage of IdP's machinery to release attributes. 
* Ability to configure an expiration and revocation policy around OIDC access and refresh tokens from an admin perspective. 

Note that no significant UI enhancements are taken into account. All configuration and changes are directly assumed to be applied to the IdP config without the presence of a web interface to facilitate. This includes administration and management of metadata, authZ codes and more.

### Resources
* http://openid.net/specs/openid-connect-basic-1_0.html
* http://openid.net/specs/openid-connect-implicit-1_0.html
 
### Planned

The following may be considered in future versions:

* Dynamic discovery
* Implicit flow
* Hybrid flow
* Dynamic RP registration
* Logout
* Web UIs that facilitate managing tokens, whitelisted/blacklisted RPs, etc. 

### Toolkit
[MITREid Connect](https://github.com/mitreid-connect/) will be used as a starting point and a foundation on top of which
adaptors will be built to close the gap.

## Versions
- [Shibboleth Identity Provider v3.1.3-SNAPSHOT](https://wiki.shibboleth.net/confluence/display/IDP30/Home)
- Apache Maven v3.x
- JDK 8

## Build [![Build Status](https://travis-ci.org/uchicago/shibboleth-oidc.svg?branch=master)](https://travis-ci.org/uchicago/shibboleth-oidc)
In order to run the overlay build, examine the `/conf/idp.properties` inside the `idp-webapp-overlay` module,
and adjust the values of hostname, entityId, passwords, etc. Then from the command prompt, execute:

### Initial installs

```bash
mvn clean install -P new
```

This will wipe out any previous files inside `credentials` and `metadata` directories and start anew.


### Subsequent installs

```bash
mvn clean install
```

## Run

### Prepare HTTPS

You will also need to set up a keystore under `/etc/jetty` and name it `thekeystore`. The keystore password and the key password should both be `changeit`.
 
A sample keystore is provided under the `idp-webapp-overlay/etc/jetty` directory that is empty, and can be used to set up the environment. 

### Run Jetty
From the root directory, run the following command:

```bash
mvn verify -Dhost=jetty
```

This will spin up an embedded Jetty server to load the IdP context. Remote debugging is available under port 5000 from your IDE. 
 
