 FHIR StructureDefinitions for Mother and Child Health Survey

This repository contains three FHIR `StructureDefinition` profiles focused on capturing patient demographics, nutrition-related questionnaires, and vital observations for mother and child health programs. These profiles are customized for use in health information systems aligned with HL7 FHIR R4 standards.

 Files Overview

   1. `demographics.json`
- **StructureDefinition ID:** `PatientProfile`
- **FHIR Resource Type:** `Patient`
- **Purpose:** Captures basic demographic information including name, gender, birth date, address, contact, and preferred language.
- **Extensions Used:**
  - `http://example.org/fhir/StructureDefinition/nepali-ethnicity`: Captures ethnicity information specific to Nepali populations.
- **Special Feature:**
  - Uses an **extension slice** on `Patient.extension` to add ethnicity-specific information.



  2. `nutrition-dietary-questionnaire.json`
- **StructureDefinition ID:** `MotherChildNutritionSurvey`
- **FHIR Resource Type:** `Questionnaire`
- **Purpose:** Models a nutrition and dietary questionnaire for both mothers and children.
- **Data Types Used:** `boolean`, `integer`, `string`
- **Extensions Used:**
  - `http://example.org/fhir/StructureDefinition/himsCode`: Associates questions with specific HIMS (Health Information Management System) codes for data reporting and integration.



  3. `observation.json`
- **StructureDefinition ID:** `MotherChildVitalsProfile`
- **FHIR Resource Type:** `Observation`
- **Purpose:** Represents combined vital signs of mother and child in a single observation entry.
- **Category:** `vital-signs`
- **Special Feature:**
  - Implements **slicing** on `Observation.component` to allow structured entries for multiple types of vitals (e.g., weight, MUAC, BMI).



What is Slicing?

"Slicing" in FHIR allows you to split a repeating element (e.g., `component[]`, `extension[]`) into uniquely identifiable sub-parts ("slices") using a **discriminator** (such as a code or pattern).

 Why Was Slicing Used Here?

In `observation.json`, slicing was applied to `Observation.component`:
 json
"component": {
  "slicing": {
    "discriminator": [{ "type": "pattern", "path": "code.text" }],
    "ordered": false,
    "rules": "open"
  }
}
This allows the creation of distinct components for:

Mother - Body Weight

Mother - BMI

Child - Body Weight

Child - MUAC

Child - Abdominal Circumference

Each of these is uniquely identified by code.text and can be validated individually.

Without slicing, repeated components could not be explicitly differentiated.

 `FHIR Version`
All profiles are based on: FHIR R4 (4.0.1)

` Publisher`

Example Publisher (Demographics, Questionnaire)

 `Use Case Summary`
These FHIR profiles are intended to:

Streamline data collection for public health surveys.

Ensure consistent interoperability across electronic health systems.

Support automated analysis by standardizing data types and formats.
Ministry of Health - Nepal (Vitals)

 `Contact`
For more information or integration help, please contact:

Ministry of Health - Nepal
FHIR Interoperability Team
