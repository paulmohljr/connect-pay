# Getting Started
[//]: <> (This is where you will want to do a brief overview of ConnectPay and what it does to help clients at Fiserv)
Update here

# Information on Integration
while we know you have various ways to integrate, we are here to assist you in integrating with us here at Fiserv. If you have 
[//]: <> (You will want to step through the integration process. You will need to create paths that are common for any and all merchants. Where there are differences, we will want to fork them using sub steps with ### instead of the ## for category headings. But, it will be necessary to understand the actual process first.)
# API Integration
## Step 1 - Create a Profile 
[//]: <> (Include in this create session token)
## Step 2 - Encryption
### AES Encryption
| Type | Value            | 
|------|------------------|
|ALGO  |AES               | 
|CIPHER| AES/GCM/NoPadding|

```java
public class AesUtil {
private static final String ALGO = "AES";
private Cipher cipher = null;
private SecretKey secretKey = null;
private String initializationVector = null;
private String correlationId = null;
public static final int GCM_TAG_LENGTH_BIT = 128;
private static final int IV_LENGTH_BYTE = 12;
/**
* Initialize cipher with IV and secret key
*/
public void init(String encKey, String initializationVector, String correlationId) throws Exception {
try {
cipher = Cipher.getInstance(PartnerAlgo.AES_GCM_NoPadding.getValue());
} catch (NoSuchAlgorithmException | NoSuchPaddingException e) {
LOG.error("Exception in AesUtil.init {}", e);
throw e;
}
this.secretKey = generateKey(encKey);
this.initializationVector = initializationVector;
this.correlationId = correlationId;
}
/**
* encryption with secret key, IV and salt (IV value)
*/
public String encrypt(String clearText, String correlationId) throws Exception {
if (this.correlationId == null)
this.correlationId = correlationId;
try {
byte[] encrypted = doFinal(Cipher.ENCRYPT_MODE, secretKey, initializationVector,
clearText.getBytes("UTF-8"));
byte[] IV_BYTES = hex(initializationVector);
byte[] cipherTextWithIv = ByteBuffer.allocate(IV_BYTES.length + encrypted.length).put(IV_BYTES)
.put(encrypted).array();
return base64(cipherTextWithIv);
} catch (UnsupportedEncodingException e) {
LOG.error("Exception in AesUtil.encrypt {}", e);
throw e;
} catch (Exception e) {
LOG.error("Exception in AesUtil.encrypt {}", e);
throw e;
}
}
private SecretKey generateKey(String encKey) {
try {
SecretKey key = new SecretKeySpec(hex(encKey), ALGO);
return key;
} catch (NumberFormatException | DecoderException e) {
LOG.error("Exception in AesUtil.generateKey {}", e);
return null;
}
}
private byte[] doFinal(int encryptMode, SecretKey key, String iv, byte[] bytes) throws Exception {
cipher.init(encryptMode, key, new GCMParameterSpec(GCM_TAG_LENGTH_BIT, hex(iv)));
return cipher.doFinal(bytes);
}
```
### AES Decryption
```java
public class AesUtil {
private static final String ALGO = "AES";
private Cipher cipher = null;
private SecretKey secretKey = null;
private String initializationVector = null;
private String correlationId = null;
public static final int GCM_TAG_LENGTH_BIT = 128;
private static final int IV_LENGTH_BYTE = 12;
/**
* Initialize cipher with IV and secret key
*/
public void init(String encKey, String initializationVector, String correlationId) throws Exception {
try {
cipher = Cipher.getInstance(PartnerAlgo.AES_GCM_NoPadding.getValue());
} catch (NoSuchAlgorithmException | NoSuchPaddingException e) {
LOG.error("Exception in AesUtil.init {}", e);
throw e;
}
this.secretKey = generateKey(encKey);
this.initializationVector = initializationVector;
this.correlationId = correlationId;
}
/**
* Decryption with secret key, IV and salt (IV value)
*/
public String decrypt(String ciphertext) throws Exception {
try {
ByteBuffer buffer = ByteBuffer.wrap(base64(ciphertext));
byte[] iv = new byte[IV_LENGTH_BYTE];
buffer.get(iv);
byte[] extractedCipherText = new byte[buffer.remaining()];
buffer.get(extractedCipherText);
byte[] decrypted = doFinal(Cipher.DECRYPT_MODE, secretKey, initializationVector, extractedCipherText);
return new String(decrypted, "UTF-8");
} catch (UnsupportedEncodingException e) {
LOG.error("Exception in AesUtil.decrypt {}", e);
throw e;
} catch (Exception e) {
LOG.error("Exception in AesUtil.decrypt {}", e);
throw e;
}
}
private SecretKey generateKey(String encKey) {
try {
SecretKey key = new SecretKeySpec(hex(encKey), ALGO);
return key;
} catch (NumberFormatException | DecoderException e) {
LOG.error("Exception in AesUtil.generateKey {}", e);
return null;
}
}
private byte[] doFinal(int encryptMode, SecretKey key, String iv, byte[] bytes) throws Exception {
cipher.init(encryptMode, key, new GCMParameterSpec(GCM_TAG_LENGTH_BIT, hex(iv)));
return cipher.doFinal(bytes);
}
}

```
## Step 3
## Step 4
## Step 5
## Step 6
## Step 7
## Step 8
## Step 9
## Step 10

# SDK Integration
## IOS
## Android
## Other? 
###Is my edit on this documentation
### Useful Artifacts to help you Integrate
[//]: <> (Need to link below to the actual files)
- [Implementation*Guide](../documentation/implementationguide.md)
- [SDK](../assets/connect-pay_spec.zip)
- [Postman Collection](../assets/connect-pay_postman.zip)
