#Self-Signed Certificate Generator
Self-signed ssl certificates can be used to set up temporary ssl servers. You can use it for test and development servers where security is not a big concern. Use the form below to generate a self-signed ssl certificate and key.

	Server name:  
	
#About SSL Certificates
SSL certificates are required in order to run web sites using the HTTPS protocol. For professional web sites, you usually buy such a certificate from Verisign, Thawte or any other ssl certificate vendor. SSL certificates use a chain of trust, where each certificate is signed (trusted) by a higher, more credible certificate. At the top of the chain of trust are the root certificates, owned by Verisign and others. These certificates are typically shipped with your operating system or web browser.
#In Internet Explorer and Firefox
When you visit a web site over HTTPS, your web browser will receive the ssl certificate for the web site. It will examine the contents of the certificate to see that is indeed valid for the domain name you are trying to visit. After that, it will verify the chain of trust. It will look at who has signed the certificate. If that certificate is a root-certificate, it will compare it against the ones shipped with the operating system. If it is a non-root certificate, it will follow the chain of trust up one more level.
#Self-signed certificates
When using a self-signed certificate, there is no chain of trust. The certificate has signed itself. The web browser will then issue a warning, telling you that the web site certificate cannot be verified. Therefore, you should not use self-signed certificates for professional use, as your visitors will not trust your web site to be safe.
#Buying a certificate
A real certificate is safer than a self-signed. If you wish to buy a real SSL certificate, click here. 