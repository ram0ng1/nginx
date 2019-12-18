Configurando um certificado SSL da Comodo (Positive SSL)
=================================

Eu uso o certificado SSL da [Superdominios.org](https://www.superdominios.org/home/cart.php?a=confproduct&i=2) que revende certificados da [Comodo](https://www.comodo.com/) por preços à partir de R$39.99 Anuais.

Essas são as etapas que eu passei para razlizar a instalação do certificado

Comprei o certificado
-----------------

Antes de comprar um certificado, você precisa gerar uma chave privada e um arquivo CSR
(Solicitação de assinatura de certificado, em Inglês Certificate Signing Request). Você será solicitado a fornecer o conteúdo do arquivo CSR
ao solicitar o certificado.

    openssl req -new -newkey rsa:2048 -nodes -keyout private.key -out exemplo.csr

Isso fornece dois arquivos:

* ``private.key`` -- sua chave privada. Você precisará disso mais tarde para configurar o nginx.
* ``www_exemplo_com.csr`` -- Seu arquivo CSR.

Agora, adquira o certificado, siga as etapas no site deles e você deverá obter em breve um
e-mail com o seu *Certificado PositiveSSL*. O e-mail deve conter um arquivo zip com o seguinte:

* Root CA Certificate - `AddTrustExternalCARoot.crt`
* Intermediate CA Certificate - `COMODORSAAddTrustCA.crt`
* Intermediate CA Certificate - `COMODORSADomainValidationSecureServerCA.crt`
* Your PositiveSSL Certificate - `www_exemplo_com.crt` (ou o subdomínio que você forneceu)

Instalando o Certificado Comodo (Positive SSL)
----------------------------

Combine tudo para o nginx:

1. Combine os arquivos `.crt` acima em um pacote (a ordem é importante aqui):

    `cat www_exemplo_com.crt COMODORSADomainValidationSecureServerCA.crt  COMODORSAAddTrustCA.crt AddTrustExternalCARoot.crt > ssl-bundle.crt`

2. Armazene o pacote onde quer que o nginx o encontre (Opcional):

    `mkdir -p /etc/nginx/ssl/example_com/`
    
    `mv ssl-bundle.crt /etc/nginx/ssl/example_com/`

3. Verifique se sua chave privada está em algum lugar que o nginx também pode lê-lo.:

    `mv exemplo_com.key /etc/nginx/ssl/exemplo_com/`

4. Verifique se a sua configuração do nginx aponta para o arquivo `ssl-bundle.crt` certo e para o arquivo `private.key` que você gerou anteriormente.

A configuração deve-se paracer como abaixo:

    `server {
        listen 443;

        ssl on;
        ssl_certificate /etc/nginx/ssl/example_com/ssl-bundle.crt;
        ssl_certificate_key /etc/nginx/ssl/example_com/exemplo_com.key;

        # side note: only use TLS since SSLv2 and SSLv3 have had recent vulnerabilities
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

        # ...

    }`

6. Reinicie o nginx.

`service nginx restart`
