//Used https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/ for reference


#include <stdio.h>
#include <string.h> 

// Function to parse HL7 ORU message 
void parseHL7Message(char *message) { 
char *token = strtok(message, "|"); 
int fieldCount = 1; 

// Variables to store parsed information 
char *patientID, *observationDate, *resultsName, *resultsValue, *resultsUnit, *resultsRange, *resultsFlag; 

//Used https://press.rebus.community/programmingfundamentals/chapter/case-control-structure/#:~:text=A%20case%20or%20switch%20statement,execution%20via%20a%20multiway%20branch. to understand case control structure below

while (token != NULL) 
{ switch (fieldCount) { 
case 1: patientID = token; break; 
case 2: observationDate = token; break; 
case 3: resultsName = token; break; 
case 4: resultsValue = token; break; 
case 5: resultsUnit = token; break; 
case 6: resultsRange = token; break; 
case 7: resultsFlag = token; break;
 
default: 
break; 

} 


token = strtok(NULL, "|"); fieldCount++; } 

//Used https://stackoverflow.com/questions/9026980/what-does-s-and-d-mean-in-printf-in-the-c-language for info on the %s below 
// Display parsed information in delimited format
printf("%s|%s|%s|%s|%s|%s|%s\n", patientID, observationDate, resultsName, resultsValue, resultsUnit, resultsRange, resultsFlag); } 
 
 int main() { 
 // Example HL7 ORU message
 char hl7Message[] = "MSH|^~\\&|NOVA^Prime+^V1.14.1057.0^PP1719210C^PRIME_PLUS_BUN_MODEL||||20220215083327.245||ORU^R01^ORU_R01|0215083327.245|P|2.5||||||UNICODE UTF-8|" "PID|1|fid:5821314|||Claw^Bear^||19860717|U|||||||||||" "PV1|1|U|||||1^Margolis^Dr.^Jeffrey|||||||||||||" "SPM|1|||BLD|||||||P||||||20220215083128.000|" "OBR|1|||^^^^Full Panel^NOVABIO|||||||||||BLD|1^Margolis^Dr.^Jeffrey|||||||||F|||||||||" "OBX|1|FT|^^^pH^pH^NOVABIO^M||7.415||7.310 to 7.410|H|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|2|FT|^^^pCO2^pCO2^NOVABIO^M||40.0|mmHg|41.0 to 51.0|L|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|3|FT|^^^Na^Na^NOVABIO^M||142.0|mmol/L|136.0 to 146.0|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|4|FT|^^^K^K^NOVABIO^M||3.86|mmol/L|3.50 to 5.10|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|5|FT|^^^Cl^Cl^NOVABIO^M||106.6|mmol/L|98.0 to 106.0|H|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|6|FT|^^^Ca^iCa^NOVABIO^M||1.25|mmol/L|1.09 to 1.35|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|7|FT|^^^Mg^iMg^NOVABIO^M||0.65|mmol/L|0.45 to 0.60|H|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|8|FT|^^^Glu^Glu^NOVABIO^M||89|mg/dL|65 to 95|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|9|FT|^^^Creat^Creat^NOVABIO^M||0.7|mg/dL|0.6 to 1.3|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|10|FT|^^^BUN^BUN^NOVABIO^M||15|mg/dL|7 to 18|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000|" "OBX|11|FT|^^^TCO2^TCO2^NOVABIO^M||27.1|mmol/L|22.0 to 29.0|N|||F|||20220215083128.000||||PP1719210C|20220215083128.000"; 
 
 // Parse the HL7 message 
 parseHL7Message(hl7Message)


 //SQL BELOW

 @echo off 
setlocal enabledelayedexpansion 

set "Aaron=root" 
set "MIEPass23=root" 
set "HL7Parsing=hl7_db" 
set "HL7Results=hl7_results" 

//Create MySQL database and table 
mysql -u %Aaron% -p%MIEPass23% -e "CREATE DATABASE IF NOT EXISTS %HL7Parsing%;" 
mysql -u %Aaron% -p%MIEPass23% %HL7Parsing% -e "CREATE TABLE IF NOT EXISTS %HL7Results% ( 

	PatientID VARCHAR(255), 
	ObservationDate VARCHAR(255), 
	ResultsName VARCHAR(255), 
	ResultsValue VARCHAR(255), 
	ResultsUnit VARCHAR(255), 
	ResultsRange VARCHAR(255), 
	ResultsFlag VARCHAR(255) 
);" 

//Process HL7 files in the directory 
	mysql -u %Aaron% -p%MIEPass23% %HL7Parsing% -e "INSERT INTO %HL7Results% VALUES;"

	) 

) 

echo Processing completed. 

:: Example Queries 
 
SELECT * FROM %HL7Results% WHERE ResultsName = 'pH'
 
SELECT * FROM %HL7Results% WHERE ResultsValue > 10; 
