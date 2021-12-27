# Virtual Log File
Transaction Log file is the only place where all the database changes are recorded. These files are used to write/log each and every event 
happening in the database in a manner that first the changes are logged and then those changes or events are actually executed. 
This phenomenon is known as “Write Ahead Logging”.

For instance, if you have started a transaction and it has to update some records in the table(s). So, SQL Server will first write the 
change in the Log file that it is going to update those specific records and then execute the changes in the memory. After the data has 
been updated, log is updated again that the transaction has been completed. So, if the SQL Server crashes in between the transaction, 
SQL Server recovery process starts the database after the crash and reads from the log to recover accordingly. This is the reason that 
if the SQL Server log file is damaged or lost, then it is almost impossible to recover the database and we have to apply more methods 
to recover the database in a stable possible which might include data loss.

# What is a Virtual Log File?
SQL Server internally manages the Log file into multiple smaller chunks called Virtual Log Files or VLFs. 
A Virtual Log File is a smaller file inside Log file which contains the actual log records which are actively 
written inside them. New Virtual Log Files are created when the existing ones are already active and new 
space is required. This brings us to the point where the value of the Virtual Log Files is created. So, whenever 
there is a crash and recovery condition, SQL Server first needs to read the Virtual Log File. Certainly, if 
the number of Virtual Log Files is huge then the time taken by the recovery will also be huge which we do not want.


# How to monitor Virtual Log File?
Monitoring Virtual Log Files is very easy. There is a very simple script from Kev Riley on Microsoft TechNet site here. 
The script will help you monitor the Virtual Log Files for your databases. The result of the query is pretty simple, 
i.e. the database name and the Virtual Log File count.

So, we should keep the monitoring the number of Virtual Log Files and keep them at a low number. We cannot say for Virtual Log Files that a specific number is accurate. Generally speaking, for every 10 Gigs of Log file we should not exceed 50 Virtual Log Files.

So, after reviewing these files, if you have more than 100 Virtual Log Files then try to check the growth settings.

If you have more than 1,000 Virtual Log Files, then first apply the fix and take preventive measures as well. The fix is also mentioned later in this article.


# How to fix Virtual Log File problems
So, now you have a pretty good idea about what is Virtual Log File and what problems it could cause. And you must have run 
the script to check your database VLFs. If you found that you have a high number of Virtual Log Files, then you might be at 
risk, but don’t worry, the solution is pretty simple.

Just shrink the Log File and re-grow it again. But there is a catch that might require a downtime so just keep it in mind 
it’s not really very easy to shrink the Log file all the time. So follow mentioned below steps and you will most probably 
be in a safe position.

1. Backup the Transaction Log file if the recovery model of the database is FULL (which generally speaking should be 
   FULL for all production databases for good recovery processes).
2. Issue a CHECKPOINT manually so that pages from the buffer can be written down to the disk.
3. Make sure there are no huge transactions running and keeping the Log file full.
4. Shrink the Log file to a smaller size
5. Re-grow the log file to a larger size on which your log file generally keeps on working.
 
That’s all! You will have a very low number of Virtual Log Files as of now.

# How to prevent Virtual Log File problem
So far you have seen how to fix the problem of the high number of Virtual Log Files but if your data is growing 
and you have a high volume of transactions (which most of us have and that is the main purpose of the database) 
then you might reach to the same position very shortly, if you do not take preventive measures for this problem.

The preventive measures are also very easy and do NOT require any downtime. Just make sure that you have updated 
the Initial Log file size to at least 1GB or to the normal operation size. This can be 20GB or whatever you might 
think it is suitable. Also, the most critical part is to fix the Growth Rate of the Log file. This should be at 
least 1 GB or higher based on your database usage. Under 1 GB is not recommended for medium to high databases.
