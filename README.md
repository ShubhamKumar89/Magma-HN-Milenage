# Magma HN Milenage

![image](https://user-images.githubusercontent.com/97805339/202797988-4f44cc5d-fbdb-4fe8-9e97-d09cde53c407.png)

![image](https://user-images.githubusercontent.com/97805339/202798057-f8359f87-122a-44d7-8343-6ec0a434cb78.png)

Source: https://www.etsi.org/deliver/etsi_ts/133100_133199/133102/11.05.01_60/ts_133102v110501p.pdf <br>
Section: 3.2

## Generating 5G Authentication Vectors

This code generates magma 5g authentication vectors such as RAND, XRES*, AUTN, and Kseaf key using different parameters.

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202798186-3da8f5f7-f742-4ac4-818d-fbdfc8a9505b.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L56

## Generating SQN

SQN is derived by adding some SEQ(Sequence Number) and IND(Index) Values.

![image](https://user-images.githubusercontent.com/97805339/202798497-dd02fbaf-7b3a-4216-8ebb-3d4b83b58d11.png)

![image](https://user-images.githubusercontent.com/97805339/202798522-a047908f-08b0-4c09-ad57-18fe1808511b.png)

![image](https://user-images.githubusercontent.com/97805339/202798548-4b7d577a-516c-4fbe-9d4c-4f8dfbc12715.png)

![image](https://user-images.githubusercontent.com/97805339/202798564-41cad31a-f418-47ad-8212-5efd07810001.png)

Source: https://www.etsi.org/deliver/etsi_ts/133100_133199/133102/11.05.01_60/ts_133102v110501p.pdf <br>
Section: C.1.1.1, C.1.1.2, C.1.2, C.3.2

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202798664-d0f6f944-0858-4303-a2aa-027490fd127e.png)

Source: https://github.com/magma/magma/blob/master/lte/gateway/python/magma/subscriberdb/processor.py#L323

## Generating RAND

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202798715-434cbbf5-92c3-4c70-a1a1-25b070b4a7ae.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L292

## Generating OPc

OPc(*Derived operator code unique for each SIM*) is derived from OP(*Operator Code*) and K(*Secret Key*). OP and K are first encrypted using AES-128 Encryption Algorithm in CBC(*Cipher block Chaining*) Mode and then the output(*opc*) and the OP are taken as input into the XOR function to derive OPc.

![image](https://user-images.githubusercontent.com/97805339/202798840-ca80429b-6bdd-4fc4-abea-ef7e72accd69.png)

Source: https://www.etsi.org/deliver/etsi_ts/135200_135299/135206/09.00.00_60/ts_135206v090000p.pdf <br>
Section: 2.3

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202798892-920b37dc-9ac2-4179-a76d-91519ddbb8d5.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L301

![image](https://user-images.githubusercontent.com/97805339/202798940-083a9964-ae8b-4842-983a-025d4c2c914d.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L342

![image](https://user-images.githubusercontent.com/97805339/202799147-d899b335-60d5-4fca-afaf-2d9e515f3259.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L431

## Generating MAC-A and MAC-S

MAC-A(*Network Authentication Code*) and MAC-S(*Resynchronisation Authentication Code*) are generated from Secret Key, SQN, RAND, OPc, and AMF using f1 and f1* cryptographic implementations through a single f1 function.

![image](https://user-images.githubusercontent.com/97805339/202799246-9da653c4-369f-41bf-8b38-ac2eed75d0c9.png)

Source: https://www.etsi.org/deliver/etsi_ts/135200_135299/135206/09.00.00_60/ts_135206v090000p.pdf <br>
Section 2.3

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202799292-ff80eccd-b3a3-46db-9093-99a68f69d16b.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L47

![image](https://user-images.githubusercontent.com/97805339/202799307-fc823ad1-e007-4997-9ea8-7ef8afdeb5f3.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L130

## Generating XRES and AK

The XRES(*Expected Response*), and AK(*Anonymity Key*)  are derived from RAND, OPc, and K using f2 and f5(or f5*) cryptography functions respectively. As the same inputs are used for deriving both parameters, a single operation is constructed for their implementation.

![image](https://user-images.githubusercontent.com/97805339/202799461-56a23b21-bf90-48da-ab84-7912b015f1b1.png)

Source: https://www.etsi.org/deliver/etsi_ts/135200_135299/135206/09.00.00_60/ts_135206v090000p.pdf <br>
Section 2.3

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202799499-67e4b478-5150-4ea0-b15c-72fe4ccd486a.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L79

![image](https://user-images.githubusercontent.com/97805339/202799523-3b0f1ea4-1a6a-492c-93d2-986f04699958.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L164

## Generating CK

CK(Ciphering Key) is derived from the Secret Key(K), RAND, and OPc using the f3 cryptography function.

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202799565-c188c72e-1619-4f83-b33d-af050dd02275.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L80

![image](https://user-images.githubusercontent.com/97805339/202799588-78201c43-24ed-4e79-adc1-34d5879191d8.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L189

## Generating IK

IK(*Integrity Key*) is derived from the Secret Key(K), RAND, and OPc using the f4 cryptography function.

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202799709-ba78fae2-08d2-4705-89b2-a9305aedf721.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L81

![image](https://user-images.githubusercontent.com/97805339/202799744-83ad8f93-c3e8-4ad5-8a87-92e08dacb808.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L213

## Generating AUTN

An Authentication Token(AUTN) is generated from the SQN, AK, MAC-A, and AMF. SQN and AK are inserted into the XOR function and the output is combined with the AMF and MAC-A.

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202799783-40c0d2ca-acb6-4132-9b55-05d96109ea6a.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L83

![image](https://user-images.githubusercontent.com/97805339/202799809-2bb08255-74b9-495f-ac16-b193cf17477e.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L314

![image](https://user-images.githubusercontent.com/97805339/202799845-94b7bb21-733a-4862-8229-dea8ef1c65d9.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L431

## Generating XRES*

XRES* is generated from CK, IK, SNNi(*Serving Network Name Identity*), RAND, and XRES. First, a key is obtained by combining CK and IK then SNNi, RAND, and XRES length are converted into an array of bytes of size 2 with the first element stored as MSB(*Most Significant Bit*). Outputs from these operations are stored independently in different variables which are further combined with FC(*it contains a byte object which is obtained from converting a hexadecimal string 6B*) to form another new variable ‘S’.

Then, S and key are inserted as input into the HMAC-SHA-256 algorithm to obtain XRES*.

![image](https://user-images.githubusercontent.com/97805339/202799971-95d42ae1-b09b-4b6a-b5ef-42e7135aede8.png)

Source: https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.03.00_60/ts_133501v160300p.pdf <br>
Section: A.4

![image](https://user-images.githubusercontent.com/97805339/202799995-24a9e8f9-f3e6-48d9-9a9b-1f5532b9bee8.png)

Source: https://www.etsi.org/deliver/etsi_ts/133200_133299/133220/14.01.00_60/ts_133220v140100p.pdf <br>
Section: B.2.0

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202800033-6e1a7d9c-cd06-4bbc-9af4-a66ca4c95fd3.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L84

![image](https://user-images.githubusercontent.com/97805339/202800057-7ee615b8-8fd6-457b-a19b-14d1caafc447.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L357

![image](https://user-images.githubusercontent.com/97805339/202800083-ddf081cc-589d-4718-b373-65e7e4567a1d.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L329

![image](https://user-images.githubusercontent.com/97805339/202800104-c76856cb-7f7c-4e60-a6d3-382674217bd6.png)

Source: https://github.com/blackberry/Python/blob/master/Python-3/Lib/hmac.py#L118

## Generating Kausf Key

CK, IK, SNNi, and AUTN are encrypted in such a way as to form Kausf(*AUSF Key*). Alike XRES*, a key obtained from combining CK and Ik and stored into a variable k. Then, SNNi and RAND lengths are stored in an array of bytes using a python library. Then, these outputs are combined with FC(*it contains a byte object which is obtained from converting a hexadecimal string 6A*) to form another temporary string variable ‘S’.  

S and k are hashed using KDF hashing algorithm HMAC-SHA-256 to form Kausf.

![image](https://user-images.githubusercontent.com/97805339/202800230-f456d97e-1a44-49bd-bc4a-316977fe0c49.png)

Source: https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.03.00_60/ts_133501v160300p.pdf <br>
Section: A.2

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202800664-c46fa639-c1a4-450f-8231-36fab3d531d4.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L85

![image](https://user-images.githubusercontent.com/97805339/202800597-5ab14c0b-e4b1-4354-9cf0-45aac761fc9d.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L390

![image](https://user-images.githubusercontent.com/97805339/202800526-eb18f3b4-9163-4109-889d-c7024910988c.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L329

![image](https://user-images.githubusercontent.com/97805339/202800460-968b9160-0ab4-4a73-87a3-054fd1f9d89d.png)

Source: https://github.com/blackberry/Python/blob/master/Python-3/Lib/hmac.py#L118

## Generating Kseaf Key

Kseaf(*SEAF Key*) is obtained by integrating Kausf and SNNi through a hashing algorithm. In this derivation, Kausf acts as key(k) whereas SNNi is still disintegrated into 2 forms, one stores the value, and the other stores the length of the SNNi in an array of bytes of size 2. The resultant output is assembled with the FC(*it contains a byte object which is obtained from converting a hexadecimal string 6C*) and stored in variable ‘S’.

Then, S and key(Kausf) undergo the HMAC-SHA-256 hashing algorithm to generate Kseaf.

  ![image](https://user-images.githubusercontent.com/97805339/202800752-be1503f4-b606-43d1-b231-46ca9f111ead.png)

Source: https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.03.00_60/ts_133501v160300p.pdf <br>
Section: A.6

### Code SS:

![image](https://user-images.githubusercontent.com/97805339/202800781-fa166b44-0233-482d-a012-4fd07b5eda80.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L86

![image](https://user-images.githubusercontent.com/97805339/202800798-4cb393e6-bf8a-4368-bcd1-ba1f9f8cbaec.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L412

![image](https://user-images.githubusercontent.com/97805339/202800822-7a021e22-dbd3-428d-bc99-35f47c6e9185.png)

Source: https://github.com/magma/magma/blob/6122b3a667ba8e0c29dda827261904c1efc963ed/lte/gateway/python/magma/subscriberdb/crypto/milenage.py#L329

![image](https://user-images.githubusercontent.com/97805339/202800885-d6f6817a-c628-43c1-8e1f-69f3fac39df7.png)

Source: https://github.com/blackberry/Python/blob/master/Python-3/Lib/hmac.py#L118
