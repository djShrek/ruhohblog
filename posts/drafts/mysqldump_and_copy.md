---
title: 'Execution of a mysqldump and scp'
date: '2015-05-30'
description:
tags: [mysql, sql, servers, scp]
---

I recently encountered a bug in an application that was very hard to debug
due to the fact that the data in our respective databases were not in sync. Trying to debug the application in the linux environment was starting to become a pain, so I decided it would be easier to try to debug the issue in my local environment (MAC OSX).

So I had to do extract the data and execute a mysql dump and then copy that
file back into my local system. Once I had the file, I would be able to accurately find the bug since the local and production databases would reflect the same data. 
The first step was to use mysqldump to dump the data into a sql file. While in the production server, I type this command into the terminal:

`mysqldump -u [dbname] -p [nuc_production_db] > name_of_sql_file.sql`

Once this command is input, the terminal asks me for the password of the production database and I provide the corresponding pw. The -u flag The file takes only less than a second to generate even though it is the size of about 124mb. Now that that file the is generated, I need to copy the file back down to my local machine. I open the terminal to my local machine and use the scp command to copy the sql file from my remote server to my local server:

`scp name_of_user@ip_address:/file/to/send /where/to/put`

Example: 

`scp super_user@123.456.78.90:/home/app/superapp/5_27.sql home/Desktop`

After this command, the terminal will download the sql file to my local machine and I will be able
to import the data back to own mysql database!

For more information:

http://unix.stackexchange.com/questions/188285/how-to-copy-a-file-from-remote-server-to-local-machine
https://dev.mysql.com/doc/refman/5.0/en/mysqldump-sql-format.html