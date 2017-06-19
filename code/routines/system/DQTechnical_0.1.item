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

import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * created by talend on 2015-07-28 Detailled comment.
 *
 */
public class DQTechnical {

    /**
     * extractTitle: Returns the extracted title based on a list of titles provided
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("Mrs. Marty Smith") inStr: the string to be processed
     * 
     * {param} int(1) trimSpaces: 0 or 1 to trim spaces or not
     * 
     * {example} extractTitle(" Mrs. Marty Smith ", 1) # returns "Mrs."
     */

    public static String extractTitle(String inStr, int trimSpaces) {
        if (inStr == null) {
            return null;
        }
        Boolean debuget = false;
        String outStr = inStr;

        Pattern p = Pattern
                .compile("^\\s?((Mr|Mrs|Ms|Miss|Dr|Herr|Monsieur|Hr|Frau|A V M|Admiraal|Admiral|Air Cdre|Air Commodore|Air Marshal|Air Vice Marshal|Alderman|Alhaji|Ambassador|Baron|Barones|Brig|Brig Gen|Brig General|Brigadier|Brigadier General|Brother|Canon|Capt|Captain|Cardinal|Cdr|Chief|Cik|Cmdr|Col|Col Dr|Colonel|Commandant|Commander|Commissioner|Commodore|Comte|Comtessa|Congressman|Conseiller|Consul|Conte|Contessa|Corporal|Councillor|Count|Countess|Crown Prince|Crown Princess|Dame|Datin|Dato|Datuk|Datuk Seri|Deacon|Deaconess|Dean|Dhr|Dipl Ing|Doctor|Dott|Dott sa|Dr|Dr Ing|Dra|Drs|Embajador|Embajadora|En|Encik|Eng|Eur Ing|Exma|Sra|Exmo Sr|F|O|Father|First Lieutient|First Officer|Flt Lieut|Flying Officer|Fr|Frau|Fraulein|Fru|Gen|Generaal|General|Governor|Graaf|Gravin|Group Captain|Grp Capt|H E Dr|H H|H M|H R H|Hajah|Haji|Hajim|Her Highness|Her Majesty|Herr|High Chief|His Highness|His Holiness|His Majesty|Hon|Hr|Hra|Ing|Ir|Jonkheer|Judge|Justice|Khun Ying|Kolonel|Lady|Lcda|Lic|Lieut|Lieut Cdr|Lieut Col|Lieut Gen|Lord|M|M L|M R|Madame|Mademoiselle|Maj Gen|Major|Master|Mevrouw|Miss|Mlle|Mme|Monsieur|Monsignor|Mr|Mrs|Ms|Mstr|Nti|Pastor|President|Prince|Princess|Princesse|Prinses|Prof|Prof Dr|Prof Sir|Professor|Puan|Puan Sri|Rabbi|Rear Admiral|Rev|Rev Canon|Rev Dr|Rev Mother|Reverend|Rva|Senator|Sergeant|Sheikh|Sheikha|Sig|Sig na|Sig ra|Sir|Sister|Sqn Ldr|Sr|Sr D|Sra|Srta|Sultan|Tan Sri|Tan Sri Dato|Tengku|Teuku|Than Puying|The Hon Dr|The Hon Justice|The Hon Miss|The Hon Mr|The Hon Mrs|The Hon Ms|The Hon Sir|The Very Rev|Toh Puan|Tun|Vice Admiral|Viscount|Viscountess|Wg Cdr)\\.?\\s)(.*)$");
        Matcher m = p.matcher(inStr);

        if (m.find()) {
            outStr = m.group(2);
            if (trimSpaces == 1) {
                TalendString.talendTrim(outStr, ' ', 0);
            }
            if (debuget) {
                System.err.println("extracted title: \"" + outStr + "\"");
            }
        }

        return outStr;
    }

    /**
     * removeTitle: Returns the string without the title
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("Mrs. Marty Smith") inStr: the string to be processed
     * 
     * {param} int(1) trimSpaces: 0 or 1 to trim spaces or not
     * 
     * {example} removeTitle(" Mrs. Marty Smith ", 1) # returns "Mrs."
     */

    public static String removeTitle(String inStr, int trimSpaces) {
        if (inStr == null) {
            return null;
        }
        Boolean debuget = false;
        String outStr = inStr;

        Pattern p = Pattern
                .compile("^\\s?((Mr|Mrs|Ms|Miss|Dr|Herr|Monsieur|Hr|Frau|A V M|Admiraal|Admiral|Air Cdre|Air Commodore|Air Marshal|Air Vice Marshal|Alderman|Alhaji|Ambassador|Baron|Barones|Brig|Brig Gen|Brig General|Brigadier|Brigadier General|Brother|Canon|Capt|Captain|Cardinal|Cdr|Chief|Cik|Cmdr|Col|Col Dr|Colonel|Commandant|Commander|Commissioner|Commodore|Comte|Comtessa|Congressman|Conseiller|Consul|Conte|Contessa|Corporal|Councillor|Count|Countess|Crown Prince|Crown Princess|Dame|Datin|Dato|Datuk|Datuk Seri|Deacon|Deaconess|Dean|Dhr|Dipl Ing|Doctor|Dott|Dott sa|Dr|Dr Ing|Dra|Drs|Embajador|Embajadora|En|Encik|Eng|Eur Ing|Exma|Sra|Exmo Sr|F|O|Father|First Lieutient|First Officer|Flt Lieut|Flying Officer|Fr|Frau|Fraulein|Fru|Gen|Generaal|General|Governor|Graaf|Gravin|Group Captain|Grp Capt|H E Dr|H H|H M|H R H|Hajah|Haji|Hajim|Her Highness|Her Majesty|Herr|High Chief|His Highness|His Holiness|His Majesty|Hon|Hr|Hra|Ing|Ir|Jonkheer|Judge|Justice|Khun Ying|Kolonel|Lady|Lcda|Lic|Lieut|Lieut Cdr|Lieut Col|Lieut Gen|Lord|M|M L|M R|Madame|Mademoiselle|Maj Gen|Major|Master|Mevrouw|Miss|Mlle|Mme|Monsieur|Monsignor|Mr|Mrs|Ms|Mstr|Nti|Pastor|President|Prince|Princess|Princesse|Prinses|Prof|Prof Dr|Prof Sir|Professor|Puan|Puan Sri|Rabbi|Rear Admiral|Rev|Rev Canon|Rev Dr|Rev Mother|Reverend|Rva|Senator|Sergeant|Sheikh|Sheikha|Sig|Sig na|Sig ra|Sir|Sister|Sqn Ldr|Sr|Sr D|Sra|Srta|Sultan|Tan Sri|Tan Sri Dato|Tengku|Teuku|Than Puying|The Hon Dr|The Hon Justice|The Hon Miss|The Hon Mr|The Hon Mrs|The Hon Ms|The Hon Sir|The Very Rev|Toh Puan|Tun|Vice Admiral|Viscount|Viscountess|Wg Cdr)\\.?\\s)(.*)$");
        Matcher m = p.matcher(inStr);

        if (m.find()) {
            outStr = m.group(3);
            if (trimSpaces == 1) {
                TalendString.talendTrim(outStr, ' ', 0);
            }
            if (debuget) {
                System.err.println("name with title removed: \"" + outStr + "\"");
            }
        }

        return outStr;
    }

    /**
     * extractLastName: Returns the string without the title
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("Mrs. Marty Smith") inStr: the string to be processed
     * 
     * {param} int(1) trimSpaces: 0 or 1 to trim spaces or not
     * 
     * {example} extractLastName(" Mrs. Marty Smith ", 1) # returns "Smith"
     */

    public static String extractLastName(String inStr, int trimSpaces) {
        if (inStr == null) {
            return null;
        }
        Boolean debuget = false;
        String outStr = inStr;

        Pattern p = Pattern.compile("\\s([a-zA-Z]+)$");
        Matcher m = p.matcher(inStr);

        if (m.find()) {
            outStr = m.group(1);
            if (trimSpaces == 1) {
                TalendString.talendTrim(outStr, ' ', 0);
            }
            if (debuget) {
                System.err.println("name with title removed \"" + outStr + "\"");
            }
        }

        return outStr;
    }

    /**
     * removeNameSuffix: Returns the string without the suffix
     * 
     * {talendTypes} String
     * 
     * {Category} Data Quality
     * 
     * {param} string("Mr. Marty Smith III") inStr: the string to be processed
     * 
     * {param} int(1) trimSpaces: 0 or 1 to trim spaces or not
     * 
     * {example} removeNameSuffix(" Mr. Marty Smith III", 1) # returns "Mr. Marty Smith"
     */

    public static String removeNameSuffix(String inStr, int trimSpaces) {
        if (inStr == null) {
            return null;
        }
        Boolean debuget = false;
        String outStr = inStr;

        Pattern p = Pattern.compile("^(.*)?\\s(Jr.|Sr.|Jr|Sr.|III|IV|V)$");
        Matcher m = p.matcher(inStr);

        if (m.find()) {
            outStr = m.group(1);
            if (trimSpaces == 1) {
                TalendString.talendTrim(outStr, ' ', 0);
            }
            if (debuget) {
                System.err.println("name with suffix removed \"" + outStr + "\"");
            }
        }

        return outStr;
    }

    /**
     * isNameStringValid: Returns true or false if the string is a valid formed name: [Initial] Firstname [Initial]
     * Lastname
     * 
     * {talendTypes} Boolean
     * 
     * {Category} Data Quality
     * 
     * {param} string("Mrs. Marty Smith") inStr: the string to be processed
     * 
     * {example} isNameStringValid("Mrs. Marty Smith ") # returns true
     */

    public static boolean isNameStringValid(String inStr) {
        if (inStr == null) {
            return false;
        }
        Pattern p = Pattern.compile("^\\s?([A-Z].? )?[A-Z][a-z]* ([A-Z].? )?[A-Z][a-z]*\\s?$");
        Matcher m = p.matcher(inStr);

        if (m.matches()) {
            return true;
        }
        return false;
    }

}