// ============================================================================
//
// Copyright (C) 2006-2016 Talend Inc. - www.talend.com
//
// This source code is available under agreement available at
// %InstallDIR%\features\org.talend.rcp.branding.%PRODUCTNAME%\%PRODUCTNAME%license.txt
//
// You should have received a copy of the agreement
// along with this program; if not, write to Talend SA
// 9 rue Pages 92150 Suresnes, France
//
// ============================================================================

package routines;

import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.security.InvalidKeyException;
import java.security.Key;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.security.spec.InvalidKeySpecException;
import java.security.spec.KeySpec;
import java.util.Calendar;
import java.util.Date;
import java.util.Random;

import javax.crypto.BadPaddingException;
import javax.crypto.Cipher;
import javax.crypto.IllegalBlockSizeException;
import javax.crypto.NoSuchPaddingException;
import javax.crypto.SecretKey;
import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.DESKeySpec;
import javax.crypto.spec.SecretKeySpec;

import sun.misc.BASE64Decoder;
import sun.misc.BASE64Encoder;

/**
 * created by talend on 2016-04-08 Detailled comment.
 *
 */
public class DataMasking {

    static final String ALGO = "AES"; //$NON-NLS-1$

    static final String UNICODE_FORMAT = "UTF8"; //$NON-NLS-1$

    static final String DES_ENCRYPTION_SCHEME = "DES"; //$NON-NLS-1$

    public static final String NULL_PARAMETER_MESSAGE = "The parameter should not be null"; //$NON-NLS-1$

    public static final String EMPTY_PARAMETER_MESSAGE = "String is empty"; //$NON-NLS-1$

    static final Random random = new Random();

    static final BASE64Encoder b64Encoder = new BASE64Encoder();

    static final BASE64Decoder b64Dencoder = new BASE64Decoder();

    /**
     * createMD2: Calculate MD2 hash value from String.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} string("foo") message: The string need to be masked.
     * 
     * {example} createMD2("foo") return is d11f8ce29210b4b50c5e67533b699d02
     * 
     * @throws NoSuchAlgorithmException
     * 
     */
    public static String createMD2(String message) throws NoSuchAlgorithmException {
        if (message == null) {
            return "Input String for MD2 calculation is missing"; //$NON-NLS-1$
        } else {
            /* MD2 Calculation */
            MessageDigest md2Instance = MessageDigest.getInstance("MD2"); //$NON-NLS-1$
            md2Instance.reset();
            md2Instance.update(message.getBytes());
            byte[] result = md2Instance.digest();

            /* Return */
            StringBuffer hexString = new StringBuffer();
            for (byte element : result) {
                if (element <= 15 && element >= 0) {
                    hexString.append("0"); //$NON-NLS-1$
                }
                hexString.append(Integer.toHexString(0xFF & element));
            }
            return hexString.toString();
        }
    }

    /**
     * createMD5: Calculate MD5 hash value from String.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} string("foo") message: The string need to be masked.
     * 
     * {example} createMD5("foo") result is acbd18db4cc2f85cedef654fccc4a4d8
     * 
     * @throws NoSuchAlgorithmException
     * 
     */

    public static String createMD5(String message) throws NoSuchAlgorithmException {
        if (message == null) {
            return "Input String for MD5 calculation is missing"; //$NON-NLS-1$
        } else {
            /* Calculation */
            MessageDigest thisMD5 = MessageDigest.getInstance("MD5"); //$NON-NLS-1$
            thisMD5.reset();
            thisMD5.update(message.getBytes());
            byte[] result = thisMD5.digest();

            /* Return */
            StringBuffer hexString = new StringBuffer();
            for (byte element : result) {
                if (element <= 15 && element >= 0) {
                    hexString.append("0"); //$NON-NLS-1$
                }
                hexString.append(Integer.toHexString(0xFF & element));
            }
            return hexString.toString();
        }
    }

    /**
     * CreditCard Masking: Masks a 16 digit credit card number with a defined character from 5th to 12th place.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} string("0123456789012345") ccnum: The string needs to be masked.
     * 
     * {param} string("*") maskingChar: The masking Character.
     * 
     * {example} maskCreditCardNumber("0123456789012345","*") result is 0123********2345
     * 
     */

    public static String maskCreditCardNumber(String ccnum, String maskingChar) {
        if (ccnum == null || maskingChar == null) {
            return NULL_PARAMETER_MESSAGE;
        }
        int total = ccnum.length();
        int startlen = 4, endlen = 4;
        int masklen = total - (startlen + endlen);
        if (ccnum.length() != 16) {
            return "No Credit Card Number - length not 16 char"; //$NON-NLS-1$
        } else {

            StringBuffer maskedbuf = new StringBuffer(ccnum.substring(0, startlen));
            for (int i = 0; i < masklen; i++) {
                maskedbuf.append(maskingChar);
            }
            maskedbuf.append(ccnum.substring(startlen + masklen, total));
            String masked = maskedbuf.toString();

            return masked;
        }
    }

    /**
     * Random String: Create a random String of defined length.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} int(5) valueLength: The length of the string.
     * 
     * {example} createRandomString(5) result maybe is "1auA5","11uyd" or "A1c8j"
     * 
     */

    public static String createRandomString(int valueLength) {
        String allowedChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890"; //$NON-NLS-1$
        return createRandomString(valueLength, allowedChars);
    }

    /**
     * Random String: Create a random String of defined length.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} int(5) valueLength: The length of the string.
     * 
     * {param} String("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890") allowedChars: The Sting which
     * the chacter of random string get from.
     * 
     * {example} createRandomString(5,"a") result must be "aaaaa"
     * 
     */

    public static String createRandomString(int valueLength, String allowedChars) {
        if (allowedChars == null || allowedChars.length() == 0) {
            return "Length of allowedChars must be greater than 0 and not be null"; //$NON-NLS-1$
        }
        String rdString = ""; //$NON-NLS-1$

        if (valueLength == 0) {
            return "Length of valueLength must be greater than 0"; //$NON-NLS-1$
        } else {
            StringBuffer buffer = new StringBuffer();
            int maxChar = allowedChars.length();
            int i = 0;
            for (i = 0; i <= valueLength - 1; i++) {
                int value = random.nextInt(maxChar);
                buffer.append(allowedChars.charAt(value));
                rdString = buffer.toString();
            }
            return rdString;
        }
    }

    /**
     * Encrypt String: Encrypts a string using AES 128 .
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} String("foo") encryptString: The string to be encrypted.
     * 
     * {param} byte[]({ 'T', 'a', 'l', 'e', 'n', 'd', 's', 'S', 'e', 'c', 'r', 'e', 't', 'K', 'e', 'y' }) keyValue: the
     * key material of the secret key. The contents of the array are copied to protect against subsequent modification.
     * 
     * {example} encryptAES("foo") result is UQ0VJZq5ymFkMYQeDrPi0A==
     * 
     * @throws NoSuchPaddingException
     * @throws NoSuchAlgorithmException
     * @throws InvalidKeyException
     * @throws BadPaddingException
     * @throws IllegalBlockSizeException
     * 
     */

    public static String encryptAES(String encryptString, byte[] keyValue) throws NoSuchAlgorithmException,
            NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
        if (encryptString == null || keyValue == null) {
            return NULL_PARAMETER_MESSAGE;
        }
        if (encryptString.length() == 0) {
            return EMPTY_PARAMETER_MESSAGE;
        } else {
            Key key = new SecretKeySpec(keyValue, ALGO);
            Cipher cipher = Cipher.getInstance(ALGO);
            cipher.init(Cipher.ENCRYPT_MODE, key);
            byte[] encVal = cipher.doFinal(encryptString.getBytes());
            String encryptedValue = b64Encoder.encode(encVal);
            return encryptedValue;

        }
    }

    /**
     * Encrypt String: Decrypts a string using AES 128.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} String("foo") encryptedString: The string to be encrypted.
     * 
     * {param} byte[]("foo") keyValue: the key material of the secret key. The contents of the array are copied to
     * protect against subsequent modification.
     * 
     * {example} decryptAES("UQ0VJZq5ymFkMYQeDrPi0A==") result is "foo"
     * 
     * @throws NoSuchPaddingException
     * @throws NoSuchAlgorithmException
     * @throws InvalidKeyException
     * @throws IOException
     * @throws BadPaddingException
     * @throws IllegalBlockSizeException
     * 
     */

    public static String decryptAES(String encryptedString, byte[] keyValue) throws NoSuchAlgorithmException,
            NoSuchPaddingException, InvalidKeyException, IOException, IllegalBlockSizeException, BadPaddingException {

        if (encryptedString == null || keyValue == null) {
            return NULL_PARAMETER_MESSAGE;
        }

        if (encryptedString.length() == 0) {
            return EMPTY_PARAMETER_MESSAGE;
        } else {
            Key key = new SecretKeySpec(keyValue, ALGO);
            Cipher cipher = Cipher.getInstance(ALGO);
            cipher.init(Cipher.DECRYPT_MODE, key);
            byte[] decordedValue = b64Dencoder.decodeBuffer(encryptedString);
            byte[] decValue = cipher.doFinal(decordedValue);
            String decryptedValue = new String(decValue);
            return decryptedValue;

        }
    }

    /**
     * Encrypt String: Encrypts a string using DES .
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} String("foo") unencryptedString: The string to be encrypted.
     * 
     * {param} String("ThisIsSecretEncryptionKey") myEncryptionKey: the string with the DES key material.
     * 
     * {example} encryptDES("foo") result is DmNj+x2LUXA=
     * 
     * @throws UnsupportedEncodingException
     * @throws NoSuchAlgorithmException
     * @throws NoSuchPaddingException
     * @throws InvalidKeyException
     * @throws InvalidKeySpecException
     * @throws BadPaddingException
     * @throws IllegalBlockSizeException
     * 
     * @throws Exception
     */

    public static String encryptDES(String unencryptedString, String myEncryptionKey) throws UnsupportedEncodingException,
            NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, InvalidKeySpecException,
            IllegalBlockSizeException, BadPaddingException {
        if (unencryptedString == null || myEncryptionKey == null) {
            return NULL_PARAMETER_MESSAGE;
        }
        if (unencryptedString.length() == 0) {
            return EMPTY_PARAMETER_MESSAGE;
        } else {
            String encryptedString = null;

            String myEncryptionScheme = DES_ENCRYPTION_SCHEME;
            byte[] keyAsBytes = myEncryptionKey.getBytes(UNICODE_FORMAT);
            KeySpec myKeySpec = new DESKeySpec(keyAsBytes);
            SecretKeyFactory mySecretKeyFactory = SecretKeyFactory.getInstance(myEncryptionScheme);
            Cipher encipher = Cipher.getInstance(myEncryptionScheme);
            SecretKey key = mySecretKeyFactory.generateSecret(myKeySpec);

            encipher.init(Cipher.ENCRYPT_MODE, key);
            byte[] plainText = unencryptedString.getBytes(UNICODE_FORMAT);
            byte[] encryptedText = encipher.doFinal(plainText);
            encryptedString = b64Encoder.encode(encryptedText);

            return encryptedString;

        }
    }

    /**
     * Decrypt String: Decrypts a string using DES .
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Masking
     * 
     * {param} String("DmNj+x2LUXA=") encryptedString: the string with the DES key material.
     * 
     * {param} String("ThisIsSecretEncryptionKey") myDecryptionKey: The string to be encrypted.
     * 
     * {example} decryptDES("DmNj+x2LUXA=") result is "foo"
     * 
     * @throws InvalidKeyException
     * @throws NoSuchPaddingException
     * @throws NoSuchAlgorithmException
     * @throws InvalidKeySpecException
     * @throws IOException
     * @throws BadPaddingException
     * @throws IllegalBlockSizeException
     * 
     */

    public static String decryptDES(String encryptedString, String myDecryptionKey) throws InvalidKeyException,
            NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeySpecException, IOException, IllegalBlockSizeException,
            BadPaddingException {

        if (encryptedString == null || myDecryptionKey == null) {
            return NULL_PARAMETER_MESSAGE;
        }

        if (encryptedString.length() == 0) {
            return EMPTY_PARAMETER_MESSAGE;
        } else {
            String decryptedText = null;

            String myDecryptionScheme = DES_ENCRYPTION_SCHEME;

            byte[] keyAsBytes = myDecryptionKey.getBytes(UNICODE_FORMAT);

            KeySpec myKeySpec = new DESKeySpec(keyAsBytes);
            Cipher decipher = Cipher.getInstance(myDecryptionScheme);
            SecretKeyFactory mySecretKeyFactory = SecretKeyFactory.getInstance(myDecryptionScheme);
            SecretKey key = mySecretKeyFactory.generateSecret(myKeySpec);

            decipher.init(Cipher.DECRYPT_MODE, key);
            byte[] encryptedText = b64Dencoder.decodeBuffer(encryptedString);
            byte[] plainText = decipher.doFinal(encryptedText);

            StringBuffer stringBuffer = new StringBuffer();
            for (byte element : plainText) {
                stringBuffer.append((char) element);
            }
            decryptedText = stringBuffer.toString();
            return decryptedText;

        }

    }

    /**
     * Blurring ADD: Adds a random value from a certain range to an Integer value. Make new value random around the
     * input number
     * 
     * 
     * {talendTypes} integer
     * 
     * {Category} Data Masking
     * 
     * {param} int(1) inputvalue: To be a base value.Any return value will base this value.
     * 
     * {param} int(5) rangefrom: Minimum value which make basevalue changed.It could be a positive integer or negative
     * integer
     * 
     * {param} int(10) rangeto: Maximum value which make inputValue changed.It could be a positive integer or negative
     * integer.
     * 
     * And rangeto-rangefrom must get a positive integer or zero
     * 
     * {example}
     * 
     * blurNumber(1,5,10) result is [6,11]
     * 
     * blurNumber(1,-10,-5) result is [-9,-4]
     * 
     * blurNumber(1,-10,10) result is [-9,11]
     * 
     */

    public static int blurNumber(int basevalue, int rangefrom, int rangeto) {
        int range = rangeto - rangefrom;
        if (range < 0) {
            return basevalue;
        }
        int randomInt = random.nextInt(Math.abs(rangeto - rangefrom) + rangeto >= 0 ? 1 : -1) + rangefrom;
        return basevalue + randomInt;
    }

    /**
     * Blurring ADD: Adds a random value from a certain range to an long value. Make new value random around the input
     * number
     * 
     * 
     * {talendTypes} long
     * 
     * {Category} Data Masking
     * 
     * {param} long(1) inputvalue: To be a base value.Any return value will around this value.
     * 
     * {param} int(5) rangefrom: Minimum value which make inputValue changed.It must be a positive integer
     * 
     * {param} int(10) rangeto: Maximum value which make inputValue changed.It must be a positive integer.And
     * rangeto-rangefrom must get a positive integer or zero
     * 
     * {example} blurNumber(1,5,10) # returns any long by [-9,11]
     * 
     */

    public static long blurNumber(long inputValue, int rangefrom, int rangeto) {
        int range = rangeto - rangefrom;
        if (range < 0) {
            return inputValue;
        }
        int randomInt = random.nextInt(Math.abs(rangeto - rangefrom) + rangeto >= 0 ? 1 : -1) + rangefrom;
        return inputValue + randomInt;

    }

    /**
     * Blurring ADD: Adds a random value from a certain range to an double value. Make new value random around the input
     * number
     * 
     * 
     * {talendTypes} double
     * 
     * {Category} Data Masking
     * 
     * {param} double(1.5d) inputvalue: To be a base value.Any return value will around this value.
     * 
     * {param} int(5) rangefrom: Minimum value which make inputValue changed.It must be a positive integer
     * 
     * {param} int(10) rangeto: Maximum value which make inputValue changed.It must be a positive integer.And
     * rangeto-rangefrom must get a positive integer or zero
     * 
     * {example} blurNumber(1.5,5,10) # returns any double by [-8.5,11.5)
     * 
     */

    public static double blurNumber(double inputValue, int rangefrom, int rangeto) {
        double range = 1.0 * (rangeto - rangefrom);
        if (range < 0) {
            return inputValue;
        }
        double randomInt = random.nextDouble() * Math.abs(rangeto - rangefrom) + rangefrom;
        return inputValue + randomInt;
    }

    /**
     * Blurring ADD: Adds a random value from a certain range to an float value. Make new value random around the input
     * number
     * 
     * 
     * {talendTypes} float
     * 
     * {Category} Data Masking
     * 
     * {param} float(1.5) inputvalue: To be a base value.Any return value will around this value.
     * 
     * {param} int(5) rangefrom: Minimum value which make inputValue changed.It must be a positive integer
     * 
     * {param} int(10) rangeto: Maximum value which make inputValue changed.It must be a positive integer.And
     * rangeto-rangefrom must get a positive integer or zero
     * 
     * {example} blurNumber(1.5,5,10) # returns any integer by [-8.5,11.5)
     * 
     */

    public static float blurNumber(float inputValue, int rangefrom, int rangeto) {
        float range = 1.0f * (rangeto - rangefrom);
        if (range < 0) {
            return inputValue;
        }
        float randomInt = random.nextFloat() * Math.abs(rangeto - rangefrom) + rangefrom;
        return inputValue + randomInt;

    }

    /**
     * IP-Adress Masking: creates a random ip-address.
     * 
     * 
     * {talendTypes} string
     * 
     * {Category} Data Masking
     * 
     * {param} Empty
     * 
     * {example} createIPAddress() result maybe is 192.168.33.111
     * 
     */

    public static String createIPAddress() {

        int randomInt1 = random.nextInt(255);
        int randomInt2 = random.nextInt(255);
        int randomInt3 = random.nextInt(255);
        int randomInt4 = random.nextInt(255);

        String ip1 = String.valueOf(randomInt1);
        String ip2 = String.valueOf(randomInt2);
        String ip3 = String.valueOf(randomInt3);
        String ip4 = String.valueOf(randomInt4);

        String ip = ip1.concat(".").concat(ip2).concat(".").concat(ip3).concat(".").concat(ip4); //$NON-NLS-1$ //$NON-NLS-2$ //$NON-NLS-3$

        return ip;

    }

    /**
     * IP-Adress Masking with Domain: creates a random ip-address while keeping the domain part of the ip-address.
     * 
     * 
     * {talendTypes} string
     * 
     * {Category} Data Masking
     * 
     * {param} String("192.168.33.111") It should be a full IP address.
     * 
     * {example} createIPAddressKeepDomain("192.168.33.111") result maybe is "192.168.77.213"
     * 
     */

    public static String createIPAddressKeepDomain(String inputval) {
        if (inputval == null) {
            return NULL_PARAMETER_MESSAGE;
        }

        int firstDot = inputval.indexOf("."); //$NON-NLS-1$
        int secondDot = inputval.indexOf(".", firstDot + 2); //$NON-NLS-1$

        String substr = inputval.substring(0, secondDot);

        int randomInt1 = random.nextInt(255);
        int randomInt2 = random.nextInt(255);

        String ip1 = String.valueOf(randomInt1);
        String ip2 = String.valueOf(randomInt2);

        String ip = substr.concat(".").concat(ip1).concat(".").concat(ip2); //$NON-NLS-1$ //$NON-NLS-2$

        return ip;

    }

    /**
     * Random Date (fromYear,toYear: Returns a random date as String .
     * 
     * 
     * {talendTypes}
     * 
     * {Category} Data Masking
     * 
     * {param} int(1900) yearFrom: Start year of range
     * 
     * {param} int(2012) yearTo: end year of range
     * 
     * {example} createRandomDate(1900,2012) result should be in the range [1900,2099]
     * 
     */

    public static String createRandomDate(int yearFrom, int yearTo) {

        String yr;

        Calendar cal = Calendar.getInstance();

        int dayOfYear = random.nextInt(cal.getActualMaximum(Calendar.DAY_OF_YEAR) - 1);

        int year = random.nextInt(yearTo - yearFrom);

        if (year <= 100) {
            Integer myYear = new Integer(year);
            yr = "19" + myYear.toString(); //$NON-NLS-1$
        } else {
            Integer myYear = new Integer(year);
            yr = "20" + myYear.toString().substring(1, 3); //$NON-NLS-1$
        }

        year = Integer.parseInt(yr);

        cal.set(Calendar.YEAR, year);
        cal.set(Calendar.DAY_OF_YEAR, dayOfYear);

        Date randomDate = cal.getTime();

        return randomDate.toString();
    }

    /**
     * Default Masking (Set_DefaultValue: Returns a default value as String) .
     * 
     * 
     * {talendTypes}
     * 
     * {Category} Data Masking
     * 
     * {param} String("foo") value: The value which should be default one.
     * 
     * {example} setDefaultValue("foo") result is "foo"
     * 
     */

    public static String setDefaultValue(String value) {
        String initString = ""; //$NON-NLS-1$

        String outString = initString + value;

        int StringLength = outString.length();

        if (StringLength == 0) {
            return "No default value"; //$NON-NLS-1$
        } else {
            return outString;
        }

    }

}