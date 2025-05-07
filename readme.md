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
