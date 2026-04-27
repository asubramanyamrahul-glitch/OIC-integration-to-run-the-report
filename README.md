# OIC-integration-to-run-the-report
Flow Description:
The integration is triggered either manually or through a scheduled/event-based trigger.
Initial variables and report parameters are assigned using the Assign activity.
A request is prepared using the Map activity and sent to the report service using the Invoke (runReport) activity.
The integration evaluates the response using a Switch condition to check whether the report output is available.
If the report output is available and valid (based on size and file conditions), it proceeds to process the data.
The report output is written into a stage file for further processing.
If the report is not yet ready, the integration enters a retry loop using a While activity until the report becomes available.
Once the file is created, it is read in segments using the Stage File (readFileInSegments) activity.
The integration iterates through each record using a For Each loop:
Maps the data into the required format
Invokes a target service or database operation to insert the data
After processing all records, a notification is sent indicating completion.
The integration ends successfully.

<img width="1905" height="882" alt="image" src="https://github.com/user-attachments/assets/f8557105-fe04-4c72-a7eb-2841cd1a0cab" />

<img width="1910" height="914" alt="image" src="https://github.com/user-attachments/assets/fa51b66a-0cb1-49de-ab19-51014edfa9c2" />

<img width="1880" height="434" alt="image" src="https://github.com/user-attachments/assets/9d705561-fc72-4e13-acdb-4cc8a60fae0e" />

<img width="969" height="462" alt="image" src="https://github.com/user-attachments/assets/83ba500d-d798-4522-9431-646ed33119eb"  />
 
<img width="1026" height="329" alt="image" src="https://github.com/user-attachments/assets/ec077998-ba61-4d6a-a686-6e0c063bc62a" />

