# Regarding Assignment 2
## Notes
- Patients can be registered without even visiting.
- A prescription includes only one drug.
- There can be multiple prescriptions per visit for the same diagnosis.
- A visit may result in multiple diagnosis and multiple prescriptions.
- Diagnoses are not predefined (Doctor write them for each visit)
- Drugs are predefined set of drugs

Entity types are below:

## PATIENT
(**ID**, FirstName, LastName, DateOfBirth, PlaceOfBirth, Age, Address, Gender, Sex, HealthInsuranceID, PhysicalInsuranceCardID)

## DRUG
(**ID**, Substance, Brand, GenericName, Dosage, PkgSize)

## PRESCRIPTION
(**ID**, *PrescribedDrugID*, *PickedDrugID*, OrdinanceDate, PickUpDate, DeliveryIntervals, *VisitID*)

## DIAGNOSIS
(**ID**, Description, ICD, *VisitID*)

## VISIT
(**ID**, *PatientID*, HCP_ID, Date, CalendarQuarter, Telemedicine)

## Relations
- PATIENT-has-VISIT (1:M)
- VISIT-leads_to-DIAGNOSIS (1:M)
- VISIT-includes-PRESCRIPTION (1:M)
- PRESCRIPTION-includes-DRUG (M:1)

## Participation and Min-Max
- (partial)PATIENT(0:M)-has-(total)VISIT(1:1) 
- (partial)VISIT(0:M)-leads_to-(total)DIAGNOSIS(1:1) 
- (partial)VISIT(0:M)-includes-(total)PRESCRIPTION(1:1) 
- (total)PRESCRIPTION(1:1)-includes-(partial)DRUG(0:M) 

## To represent similar drugs
SIMILAR_DRUGS(**OriginalDrugID, SimilarDrugID**)

# Assignment 3 Assumptions
- Patients can be registered without even visiting.
- A prescription includes only one drug.
- Each visit is associated with exactly one diagnosis and one prescription.
- Diagnoses are predefined and include an ICD code.
- Drugs are a predefined set.

# Python MySQL
[Install MySQL](https://dev.mysql.com/downloads/installer/)

Choose version: 8.0.42 (353.7M) and choose the "Full" Setup

## Connector Package
In your environment, run:
```
pip install mysql-connector-python
```

In your python project:
```
from mysql import connector
db = connector.connect (
    host = "localhost",
    user = "root",
    passwd = "root",
    auth_plugin='mysql_native_password')
```

## Create a database
```
mycursor = db.cursor()
mycursor.execute("CREATE DATABASE testdatabase")
```

## Connect to the database
```
db = connector.connect (
    host = "localhost",
    user = "root",
    passwd = "root",
    auth_plugin='mysql_native_password',
    database = "testdatabase"
)
mycursor = db.cursor()
```

## Do some SQL, For example:
```
mycursor.execute("CREATE TABLE customers (name VARCHAR(255), address VARCHAR(255))")
```
```
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("John", "Highway 21")
mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record inserted.")
```

```
mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

```
sql = "SELECT * FROM customers WHERE address ='Park Lane 38'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```