# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. The format of the data present in the csv file (order of data, format of time and date, units of the battery parameters)
3. Amount of csv data stored is for a month or not (is it lower than that or exceeding that time period)
4. A working functionality or API to create a PDF file
5. Connection to an email server to send out the notification via email.


(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | We assume that the PDF converter works fine and it is not our task to test the functionality of third party                                                          -                                             applications. We mock PDF converter functionality wherever it is needed in the unit testing. 
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | We only test if the notification method is being called by using mock functionality.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the number of times of breach to the PDF, when the csv file contains value that breaches either  maximum or minimum values.
4. Write the date and time of the reading to the PDF when it keeps increasing for more than 30 minutes continuously.
5. Send a notification to the user when a new PDF file is created based on breaches or continuous increase in reading values.
6. Mimic accessing the csv file from the server and assess different exception cases.
7. Mimic sending notification to the user from an email server and assess various exception scenarios.
8. Mimic accessing the server to store PDF when csv file is processed. 



(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input          | Output                      | Faked/mocked part
|--------------------------|----------------|-----------------------------|---
Read input from server     | csv file       | internal data-structure     | Fake the server store
Validate input             | csv data       | valid / invalid             | None - it's a pure function
Notify report availability | PDF            | sent/unsent                 | Fake the notification call via email
Report inaccessible server | server path    | accessible/inaccessible     | Fake the server access
Find minimum and maximum   | csv data       | values                      | None- it’s a pure function
Detect trend               | csv data       | present/absent              | None- it’s a pure function
Write to PDF               | processed date | PDF                         | Fake the call to off-the-shelf PDF converter
