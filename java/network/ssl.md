###Certificate type
- Single Domain
    This type is meant to be used for a single domain and offers no support for subdomains. For example, if the certificate is to be used for www.phoenixnap.com,
    it will not support any other domain name.

- Multiple Domain (SAN/UC Certificates)
    Multiple domain certificates are used for numerous domains and subdomains. Besides the FQDN, you can add support for other (sub)domains by adding them to the Subject Alternative Name Field.
    For example, a SAN certificate can include the domain www.phoenixnap.com, its subdomain help.phoenixnap.com as well as another domain (e.g., www.examplesite.com).
  
- Wildcard
    Wildcard certificates can be used for a domain, including all of its subdomains. The main difference is that instead of it being issued for a specific FQDN,
    wildcard certificates are used for a wide range of subdomains. For example, a wildcard certificate issued to *.phoenixnap.com could be used for a wide range of subdomains
    under the main www.phoenixnap.com domain, as seen in the image below.
###Certificate validation type
- Domain Validation (DV)
- Organization Validation (OV)
- Extended Validation (EV)

###what Cipher suite contains
- what key exchange algorithm should be used during pre-master key exchange
- what authentication algorithm should be used during the handshake.
- what session encryption algorithm should be used to encrypt the message
- what message authentication algorithm should be used to authenticate message

###Cipher suite structure
[example cipher suite](https://ciphersuite.info/cs/TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256/)
```
 struct {
          ProtocolVersion server_version;
          Random random;
          SessionID session_id;
          CipherSuite cipher_suite;
          CompressionMethod compression_method;
          select (extensions_present) {
              case false:
                  struct {};
              case true:
                  Extension extensions<0..2^16-1>;
          };
      } ServerHello;
```

###how SSL/TLS handshake works
![SSL/TLS handshake process explained](SSLTLS_handshake.png)

###how certificate chain verification works
[reference doc](https://docs.oracle.com/cd/E19424-01/820-4811/gdzea/index.html)
Certificate chain verification is the process of making sure a given certificate chain is well-formed, valid, properly signed, and trustworthy.
Directory Server software uses the following steps to form and verify a certificate chain, starting with the certificate being presented for authentication:

1.The certificate validity period is checked against the current time provided by the verifier’s system clock.

2.The issuer’s certificate is located. The source can be either the verifier’s local certificate database (on that client or server) 
  or the certificate chain provided by the subject (for example, over an SSL connection).

3.The certificate signature is verified using the public key in the issuer certificate.

4.If the issuer’s certificate is trusted by the verifier in the verifier’s certificate database, verification stops successfully here.
  Otherwise, the issuer’s certificate is checked to make sure it contains the appropriate subordinate CA indication in the Directory Server
  certificate type extension,and chain verification returns to step 1 to start again, but with this new certificate.
 
###how to debug java application ssl
```
-Djavax.net.debug=help
-Djava.security.debug=help
#use certpath debug flag to check if there is any certificate issue
-Djava.security.debug=certpath
Here is a complete example of how to get a list of the debug options:

    java -Djavax.net.debug=help MyApp 
where MyApp is an application that uses some of the JSSE classes. MyApp will not run after the debug help information is printed, as the help code causes the application to exit.
Here are the current options:

        all        turn on all debugging
        ssl        turn on ssl debugging

        The following can be used with ssl:
            record          enable per-record tracing
            handshake       print each handshake message
            keygen          print key generation data
            session         print session activity
            defaultctx      print default SSL initialization
            sslctx          print SSLContext tracing
            sessioncache    print session cache tracing
            keymanager      print key manager tracing
            trustmanager    print trust manager tracing

        handshake debugging can be widened with:
            data            hex dump of each handshake message
            verbose         verbose handshake message printing

        record debugging can be widened with:
            plaintext       hex dump of record plaintext
            packet          print raw SSL/TLS packets
Examples
To view all debugging messages:
    java -Djavax.net.debug=all MyApp
To view the hexadecimal dumps of each handshake message, you can type the following, where the colons are optional:
    java -Djavax.net.debug=ssl:handshake:data MyApp
To view the hexadecimal dumps of each handshake message, and to print trust manager tracing, you can type the following, where the commas are optional:
    java -Djavax.net.debug=SSL,handshake,data,trustmanager MyApp
```
[JSSERefGuide](https://docs.oracle.com/javase/1.5.0/docs/guide/security/jsse/JSSERefGuide.html#Debug)
[ReadDebug](https://docs.oracle.com/javase/1.5.0/docs/guide/security/jsse/ReadDebug.html)

###jdk's default ssl certs file location
```
C:\Program Files\Java\jre1.8.0_91\lib\security\cacerts
```
###specify ssl certs file when start up jvm
```
-Djavax.net.ssl.trustStore=your trust store absolute location
-Djavax.net.ssl.trustStorePassword=your trust store password
```
###specify key store
```
javax.net.ssl.keyStore=your key store absolute location
javax.net.ssl.keyStorePassword=your key store password
```
####how to edit keystore file
```
you can use "KeyStore Explorer" application to view and edit keystore file
```
###Create a CSR and a private key without a pass phrase in a single command 

```
openssl req -nodes -newkey rsa:2048 -keyout example.key -out example.csr
```
###Use keytool to generate a self signed keystore
```
keytool -genkey -keyalg RSA -alias selfsigned -keystore keystore.jks -storepass password -validity 360 -keysize 2048
```

###Convert CRT file to PEM file
```
sudo openssl x509 -in WalmartRootCA-SHA256.crt -inform der -out walmartrootca.pem -outform PEM
```

###how to decrypt java tls(https) traffic with wireshark
- run java application with below VM options
```
-javaagent:C:\Users\vn50bj4\extract-tls-secrets-4.1.0.jar=C:\Users\vn50bj4\secrets.log
```
- in wireshark config pre-master keylog file with the above generated file(C:\Users\vn50bj4\secrets.log)
