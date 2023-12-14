#include <stdio.h>
#include <string.h>

#define MAX_BUFFER_SIZE 4096

void parseHL7Message(char *hl7Message);

int main() {
    // Replace this string with your actual HL7 ORU Message
    char hl7Message[MAX_BUFFER_SIZE] = "MSH|^~\\&|NOVA^Prime+^V1.14.1057.0^PP1719210C^PRIME_PLUS_BUN_MODEL||||20220215083327.245||ORU^R01^ORU_R01|0215083327.245|P|2.5||||||UNICODE UTF-8\nPID|1|fid:5821314|||Claw^Bear^||19860717|U|||||||||||\nPV1|1|U|||||1^Margolis^Dr.^Jeffrey|||||||||||||\nSPM|1|||BLD|||||||P||||||20220215083128.000\nOBR|1|||^^^^Full Panel^NOVABIO|||||||||||BLD|1^Margolis^Dr.^Jeffrey|||||||||F|||||||||\nOBX|1|FT|^^^pH^pH^NOVABIO^M||7.415||7.310 to 7.410|H|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|2|FT|^^^pCO2^pCO2^NOVABIO^M||40.0|mmHg|41.0 to 51.0|L|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|3|FT|^^^Na^Na^NOVABIO^M||142.0|mmol/L|136.0 to 146.0|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|4|FT|^^^K^K^NOVABIO^M||3.86|mmol/L|3.50 to 5.10|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|5|FT|^^^Cl^Cl^NOVABIO^M||106.6|mmol/L|98.0 to 106.0|H|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|6|FT|^^^Ca^iCa^NOVABIO^M||1.25|mmol/L|1.09 to 1.35|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|7|FT|^^^Mg^iMg^NOVABIO^M||0.65|mmol/L|0.45 to 0.60|H|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|8|FT|^^^Glu^Glu^NOVABIO^M||89|mg/dL|65 to 95|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|9|FT|^^^Creat^Creat^NOVABIO^M||0.7|mg/dL|0.6 to 1.3|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|10|FT|^^^BUN^BUN^NOVABIO^M||15|mg/dL|7 to 18|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000\nOBX|11|FT|^^^TCO2^TCO2^NOVABIO^M||27.1|mmol/L|22.0 to 29.0|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000";

    parseHL7Message(hl7Message);

    return 0;
}

void parseHL7Message(char *hl7Message) {
    char *token = strtok(hl7Message, "\n");

    while (token != NULL) {
        // Check if the segment contains the desired fields
        if (strstr(token, "PID") || strstr(token, "OBX.14") || strstr(token, "OBX.3") ||
            strstr(token, "OBX.5") || strstr(token, "OBX.6") || strstr(token, "OBX.7") || strstr(token, "OBX.11")) {
            char *field = strtok(token, "|");
            int fieldNum = 1;

            while (field != NULL) {
                // Check if the field number is the one we are interested in
                if (fieldNum == 3 || fieldNum == 14 || fieldNum == 5 || fieldNum == 6 || fieldNum == 7 || fieldNum == 11) {
                    printf("%s|", field);
                }

                field = strtok(NULL, "|");
                fieldNum++;
            }

            printf("\n");
        }

        token = strtok(NULL, "\n");
    }
}
