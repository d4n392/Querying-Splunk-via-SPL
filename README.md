# Querying-Splunk-via-SPL
In this introductory Splunk lab, I explored the fundamentals of SPL (Search Processing Language) indexing and applied it to search specific log events. I began by running basic search queries like _index="main" host="mailsv" fail* root_ to identify failed login attempts to the root user on the mail server. Indicating a possible _brute force_ attack I then shifted gears to analyze data from a vendor sales server by querying _index="main" host=vendor_sales"_.
This lab helped me gain a practical understanding of how to search through indexed data and refine my results based on specific hosts and keywords, improving my ability to detect potential security incidents or system failures.

### Step 1: Query the Main Index for All Events
SPL Query: _index="main"_

This query fetches all events logged in the main index. It is the starting point for gathering unfiltered log data, which can be used to analyze general activity. Running this query helps identify broad trends or system-wide behaviors before applying filters.

![Screenshot 2024-09-07 132402](https://github.com/user-attachments/assets/025f40cd-a5fd-4e03-ae6a-a9a6d5a05468)
_These results displayed all recorded events in the _"main"_ index, showing log data across different hosts and sources. Expect to see varied event types, timestamps, and host details. This output serves as the base for deeper analysis._

### Step2: Query Events for Specific Host
SPL Query: _index="main" host="mailsv"_

This query focuses on retrieving all events from the _main_ index that are associated with the mailsv host. By narrowing the search to a specific host, you can analyze activities and logs for this machine exclusively, making it easier to identify patterns, issues, or anomalies related to that host.

![Screenshot 2024-09-07 132430](https://github.com/user-attachments/assets/e45989a3-8eac-48e3-9139-adf1e4ea39fc)
_The output displayed events generated by the mailsv host. Results included log data such as event type, timestamp, and associated processes or errors on the server. This information is valuable for monitoring the health and security of the mailsv server and diagnosing any issues specific to this host._

### Step 3: Search for Failed Root Login Attempts on Mail Server
SPL Query: _index="main" host="mailsv" fail* root_

This step focuses on identifying failed login attempts specifically involving the root user on the _"mailsv"_ host (mail server). Using the wildcard _fail*_, we capture all variations of failure messages, such as _"failed"_ or _"failures"_. The goal is to extract logs that highlight security vulnerabilities or unauthorized attempts.

![Screenshot 2024-09-07 132452](https://github.com/user-attachments/assets/1c260451-88fc-4049-bc66-2ec43bcbd2bb)
_The output displayed logs from the main index where failed actions have occurred on the mailsv host, specifically involving the root user. These events are crucial for identifying unauthorized access attempts, misconfigurations, or potential security vulnerabilities on the server. Logs may include failed login attempts, file access failures, or other system-related errors involving the root account. This data helps in pinpointing critical security issues and operational failures._

![Screenshot 2024-09-07 132550](https://github.com/user-attachments/assets/ba0354fd-95aa-4200-adf4-1cbe19048095)
_These results are pointing to a possible breach attempt. There are multiple failed login attempts for root from various IPs and Ports all at 1:39:51 AM. Which indicated to me a brute force attack._

### Step 4: Search for Vendor Sales Activity in Main Index
SPL Query: _index="main" host=vendor_sales_
Description:
In this step, the query is used to retrieve events related to the _"vendor_sales"_ host in the _"main"_ index. This query helps in analyzing sales-related system activity, such as monitoring the performance of the sales server or checking for any unusual behavior affecting transactions.

![Screenshot 2024-09-07 132822](https://github.com/user-attachments/assets/a332d3c4-ce93-4086-979e-c6063ee86f72)
