# PHP中openssl的使用
前段时间，有门课程的期末设计是实现一下基于B/S模式简单的CA系统。我采用了php编写后端的方式进行。其中的核心就是PHP的openssl扩展。
## CA系统的基本流程
CA是PKI系统中通信双方信任的实体，被称为可信第三方（Trusted Third Party，简称TTP）。作为可信第三方的行为具有非否认性。作为第三方而不是简单的上级，就必须能让信任者有追究自己责任的能力。CA系统首先需要一个密钥对，用于生成自签名证书，和用私钥给证书申请材料签名。使用者生成密钥对后，将公钥上传用于对证书的加密，私钥留着解密。CA系统会生成吊销证书列表（crl）文件
## PHP openssl的常用函数
openssl_csr_new（），第一个参数是dn，用于存储申请证书的信息。第二个参数是公钥，用于生成证书申请材料。  
openssl_csr_sign(),第一个参数是用于签署的证书申请材料。第二个参数是CA的根证书。第三个参数是CA系统的私钥，第四个参数是证书的有效期。  
openssl_pkey_new(),可以不设置参数，生成一个密钥对。也可以设置密钥的位数。  
openssl_okey_get_public(),该函数可以从证书中解析出公钥，只有一个参数就是证书。  
openssl_pkey_get_private()，该函数用于获取私钥，一共有两个参数。第一个参数可以是包含pem格式的证书和私钥。也可以是pem格式的私钥。第一个参数用于应对被加密的密钥。  
openssl_pkey_export_to_life()，第一个参数是密钥，第二个是生成的文件。经过我的验证，这个函数得到是私钥。  
openssl_pkey_get_details()，只有一个参数是密钥，得到的是公钥。  
openssl_x509_export_to_file（），第一个参数是证书参数，第二个参数是输出文件的路径。  
暂时主要学习的就是这些。