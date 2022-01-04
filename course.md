# Introduction to Azure Stream Analytics
This file contains text you can copy and paste for the examples in Cloud Academy's _Introduction to Azure Stream Analytics_ course.  

### Introduction
[Azure Free Trial](https://azure.microsoft.com/free)  

### Creating and Running a Job
```
SELECT 
    System.Timestamp AS EndTime,
    dspl AS SensorName,
    Avg(temp) AS Temperature
INTO
   output
FROM
    InputStream
TIMESTAMP BY time
GROUP BY SlidingWindow(second, 30), dspl
HAVING Avg(temp) > 100
```

### Running a More Complex Job
```
telcodatagen 1000 .2 2
```
If this gives you a format error, then try the following command instead:
```
telcodatagen 1000 0,2 2
```
```
SELECT  System.Timestamp as Time, 
     CS1.CallingIMSI, 
     CS1.CallingNum as CallingNum1, 
     CS2.CallingNum as CallingNum2, 
     CS1.SwitchNum as Switch1, 
     CS2.SwitchNum as Switch2 
 FROM CallStream CS1 TIMESTAMP BY CallRecTime 
     JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
     ON CS1.CallingIMSI = CS2.CallingIMSI 
     AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
 WHERE CS1.SwitchNum != CS2.SwitchNum
 ```

### Conclusion
[Azure Stream Analytics documentation](https://docs.microsoft.com/azure/stream-analytics)  
