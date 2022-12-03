# Deploy

```sh
mvn clean install -DskipTests
mvn openmrs-sdk:deploy -DserverId=dev -DartifactId=spkdzm -DgroupId=ru.spkdzm.openmrs -Dversion=1.0.0-SNAPSHOT
```

# Run

```sh
mvn openmrs-sdk:run -DserverId=dev
```

# Hot deploy webapp resources

```sh
mvn package -P deploy-web -DskipTests -Ddeploy.path=$HOME/openmrs/dev/tmp/openmrs/
```

# Form URL

http://localhost:8080/openmrs/htmlformentryui/htmlform/enterHtmlFormWithStandardUi.page?patientId=1&visitId=1&formId=1&definitionUiResource=spkdzm:cbc.xml

# Add Identifier mapping

See https://github.com/Bahmni/bahmni-core/blob/master/bahmnicore-omod/src/main/resources/liquibase.xml#L4567

```sql
set @metadata_uuid = null;
SELECT uuid INTO @metadata_uuid FROM patient_identifier_type WHERE name = "Patient Identifier";
UPDATE metadatamapping_metadata_term_mapping SET metadata_uuid=@metadata_uuid WHERE code="emr.primaryIdentifierType";
```
