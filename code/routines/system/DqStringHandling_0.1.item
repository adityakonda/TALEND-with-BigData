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

import java.util.HashSet;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Data quality String handling routines.
 */
public class DqStringHandling {

    private static final Pattern INITIALS = Pattern.compile("^[A-Z]([. &-/|][A-Z])*[. &-/|]?$"); //$NON-NLS-1$

    /**
     * containsOnlyInitials: return true if the given string only contains initials such as "A", "A.", "A.I." or
     * "A.I.D.S",.
     * 
     * 
     * {talendTypes} Boolean
     * 
     * {Category} User Defined
     * 
     * {param} string("A.I.D.S") str: The string that will be checked for initials
     * 
     * {example} containsOnlyInitials("A.I.D.S.") # true.
     */
    public static boolean containsOnlyInitials(String str) {
        if (str == null) {
            return false;
        }
        Matcher matcher = INITIALS.matcher(str);
        return (matcher.find());
    }

    /**
     * makeSafe: returns an empty string when the given string is null.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("world") str: The string to make safe.
     * 
     * {example} makeSafe("world") # world.
     */
    public static String makeSafe(String str) {
        return (str == null) ? "" : str; //$NON-NLS-1$
    }

    /**
     * safeTrim: returns the trimmed string or the empty string when the string is null.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("world") str: The string to trim (can be null).
     * 
     * {example} safeTrim("  world  ") # world.
     */
    public static String safeTrim(String str) {
        return makeSafe(str).trim();
    }

    /**
     * safeConcat: returns the concatenation of the trimmed strings. The separator character is used when none of the
     * given strings is empty or null.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("hello") str1: The string to concatenate (can be null).
     * 
     * {param} string("world") str2: The string to concatenate (can be null).
     * 
     * {param} char('|') separator: the separator to be used in the concatenation of the strings
     * 
     * {example} safeConcat("hello ","  world  ", '!') # hello|world.
     */
    public static String safeConcat(String str1, String str2, char separator) {
        String safeStr1 = safeTrim(str1);
        String safeStr2 = safeTrim(str2);
        if (safeStr1.length() == 0) {
            return safeStr2;
        } // else
        if (safeStr2.length() == 0) {
            return safeStr1;
        } // else
        return safeStr1 + separator + safeStr2;
    }

    /**
     * safeConcatMerge: returns the concatenation of the trimmed and unique strings. The separator character is used
     * when none of the given strings is empty or null. If two strings are the same, only one is concatenated. The order
     * of the output does may be different from the input order.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} char('|') separator: the separator to be used in the concatenation of the strings
     * 
     * {param} strings("hello","world") strings: The string to concatenate (can be null).
     * 
     * {example} safeConcat( '|', "hello ","  world  ", "world") # hello|world.
     */
    public static String safeConcatMerge(char separator, String... strings) {

        if (strings == null) {
            return ""; //$NON-NLS-1$
        }

        HashSet<String> hs = new HashSet<String>();
        String resultingString = ""; //$NON-NLS-1$
        for (String string : strings) {
            String safeString = safeTrim(string);
            if (hs.add(safeString)) {
                resultingString = safeConcat(resultingString, safeString, separator);
            }
        }
        return resultingString;
    }

    /**
     * safeConcat: returns the concatenation of the trimmed strings. The separator character is used when none of the
     * given strings is empty or null.
     * 
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} char("|") separator: the separator to be used in the concatenation of the strings
     * 
     * {param} strings("hello","world") strings: The string to concatenate (can be null).
     * 
     * {example} safeConcat( '|', "hello ","  world  ") # hello|world.
     */
    public static String safeConcat(char separator, String... strings) {
        if (strings == null) {
            return ""; //$NON-NLS-1$
        }
        String resultingString = ""; //$NON-NLS-1$
        for (String string : strings) {
            String safeString = safeTrim(string);
            resultingString = safeConcat(resultingString, safeString, separator);
        }
        return resultingString;
    }

    /**
     * validAscii: validate the ascii format or not
     * 
     * {talendTypes} boolean
     * 
     * {Category} User Defined
     * 
     * {param} string("text") text: The text to validate.
     * 
     * {example} validAscii("text") # true
     */
    public static boolean validAscii(String text) {
        boolean result = true;
        for (int i = 0; i < text.length(); i++) {
            int charCode = text.charAt(i);
            if (charCode < 33 || charCode > 126) {
                result = false;
                break;
            }
        }
        return result;
    }
}
