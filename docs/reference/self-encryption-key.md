# self encryption key

### Definition

Self-Encryption key is an AES symmetric key that you own for encrypting data for yourself.

### atPlatform

In the atPlatform, the self-encryption key is used to encrypt data that is stored in your own secondary server. It is crucial that this key is kept secret and owned only by you so that third parties like Atsign cannot see your data.

The self-encryption key is generated during the CRAM process when your PKAM RSA keypair is generated and your atSign is activated.

### Related Resources

\{{< card/breadcrumb href="/reference/atsign" first="atSign" >\}} \{{< card/breadcrumb href="/reference/encryption" first="Encryption" >\}} \{{< card/breadcrumb href="/reference/public-private-keys" first="Public and Private Keys" >\}} \{{< card/breadcrumb href="/reference/cram" first="CRAM" >\}} \{{< card/breadcrumb href="/reference/pkam" first="PKAM" >\}}
