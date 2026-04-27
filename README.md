

***

# OIC Integration – Run BI Publisher Report and Process Output

## 1. Integration Name

**OIC\_Integration\_To\_Run\_BIP\_Report**

***

## 2. Integration Purpose

This integration is designed to execute a BI Publisher report from Oracle Fusion using Oracle Integration Cloud (OIC), retrieve the generated report output, process the data record by record, and load it into a target system or database. The integration supports manual, scheduled, or event‑based execution and includes retry logic to handle report processing delays.

***

## 3. Trigger Mechanism

The integration can be triggered using one of the following methods:

*   **Manual trigger**
*   **Scheduled trigger**
*   **Event‑based trigger**

The trigger initializes the integration and starts the report execution process.

***

## 4. High-Level Flow Overview

1.  Initialize integration variables and report parameters.
2.  Invoke BI Publisher report service.
3.  Validate report execution status.
4.  Retry report execution if output is not ready.
5.  Write the report output to a stage file.
6.  Read the file in segments.
7.  Process each record and load it into the target system.
8.  Send completion notification.
9.  End integration successfully.

***

## 5. Detailed Flow Description

### 5.1 Assign – Initialize Variables

*   Report parameters (such as report path, template name, format, and user‑defined inputs) are initialized.
*   Control variables such as retry count, file size checks, and status flags are assigned.

***

### 5.2 Map – Prepare Report Request

*   The request payload for the **BI Publisher runReport service** is constructed.
*   All required report parameters and runtime options are mapped.

***

### 5.3 Invoke – Run Report

*   The `runReport` operation is invoked to execute the BI Publisher report.
*   The response contains report status and output metadata.

***

### 5.4 Switch – Check Report Availability

*   The integration evaluates the response to determine whether the report output is available.
*   Conditions checked include:
    *   Presence of report output
    *   Valid file size
    *   Output status

***

### 5.5 While Loop – Retry Until Report Is Ready

*   If the report output is not available, the integration enters a **While loop**.
*   The report service is re‑invoked until:
    *   The output becomes available, **or**
    *   The maximum retry count is reached.

***

### 5.6 Stage File – Write Report Output

*   Once available, the report output is written to a **stage file**.
*   The file is stored temporarily for downstream processing.

***

### 5.7 Stage File – Read File in Segments

*   The generated report file is read using the **Read File in Segments** action.
*   This ensures efficient handling of large data sets.

***

### 5.8 For Each – Process Records

*   The integration iterates through each record from the file.
*   For each record:
    *   Data is mapped into the required target format.
    *   A target service or database operation is invoked to insert or process the data.

***

### 5.9 Notification – Completion Message

*   After all records are successfully processed:
    *   A notification (email or integration response) is sent.
    *   The notification confirms successful completion of the integration.

***

### 5.10 Integration Completion

*   The integration ends gracefully with a **success status** after all steps are completed.

***

## 6. Error Handling and Reprocessing

*   Retry logic is implemented to handle delayed report availability.
*   File size and validity checks prevent processing incomplete or invalid outputs.
*   Standard fault handling is used for service invocation failures.

***

## 7. Key Benefits

*   Automated execution of BI Publisher reports
*   Scalable processing of large report outputs
*   Robust retry and validation logic
*   Reliable data loading into target systems

***

## 8. Dependencies

*   Oracle Integration Cloud
*   Oracle Fusion BI Publisher
*   Target service or database for data loading

***



<img width="1905" height="882" alt="image" src="https://github.com/user-attachments/assets/f8557105-fe04-4c72-a7eb-2841cd1a0cab" />

<img width="1910" height="914" alt="image" src="https://github.com/user-attachments/assets/fa51b66a-0cb1-49de-ab19-51014edfa9c2" />

<img width="969" height="462" alt="image" src="https://github.com/user-attachments/assets/83ba500d-d798-4522-9431-646ed33119eb"  />
 
<img width="1026" height="329" alt="image" src="https://github.com/user-attachments/assets/ec077998-ba61-4d6a-a686-6e0c063bc62a" />

***
<img width="1880" height="434" alt="image" src="https://github.com/user-attachments/assets/9d705561-fc72-4e13-acdb-4cc8a60fae0e" />

