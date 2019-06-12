# Lab 3: Work with a load-producing application on Event Streams
**Duration:** 30 minutes

In this exercise, you install another sample application that you can use to generate workloads of a specific size. You can use one of the predefined load sizes, or you can specify your own settings to test throughput.

You must complete Labs 1-2 before proceeding with this lab.

## Step 1. Install and configure the workload producer application

1. On the ICP Master virtual machine image, open Firefox and click the **IBM Cloud Private** bookmark tab, or enter the following address in a browser:

	`https://mycluster.icp:8443/`
	
2. On the IBM Cloud Private login page, log in with the user ID **admin** and password **admin**. 

3. From the hamburger menu, select **Workload > Helm Releases > eslab**.

4. Click **Launch** in the upper right corner, and then select **admin-ui-https**.

 ![Screen capture of Skytap dashboard - launch ES console](../Images/lab02-config10.png)

5. Log in with the user ID **admin** and password **admin**. 

6. Click the **Toolbox** tab to access tools.

7. Click **View on GitHub** in the Workload generation application. 

 ![Screen capture of Skytap dashboard - view on GitHub](../Images/lab03-workload1.png)
 
8. GitHub opens in a new browser tab. Scroll down to the README.md page and click **here**.

 ![Screen capture of Skytap dashboard - readme click here](../Images/lab03-workload2.png)

9. Under **Latest Release**, click **es-producer.jar** to download it to /home/student/Downloads. 

 ![Screen capture of Skytap dashboard - download producer jar](../Images/lab03-workload3.png)
 
 Select **Save file**, and click **OK**. 
 
10. In a command terminal window, change to the Downloads directory (`cd Downloads`) and run the following command:

 `java -jar es-producer.jar -g`
 
 ![Screen capture of Skytap dashboard - command output](../Images/lab03-workload4.png)
 
 This command creates the configuration file, `producer.config`.

11. Run the following command to open this file in an editor:

 `gedit producer.config`
 
 You must add some information to this file that you can find in the Event Streams console. 
 
12. In the Event Streams console, click the **Topics** tab, and then click **eslab**. 

 ![Screen capture of Skytap dashboard - eslab topic page](../Images/lab03-workload5.png)

13. Click **Connect to this topic**.

 ![Screen capture of Skytap dashboard - connect to this topic](../Images/lab03-workload6.png)
 
14. Copy the **Bootstrap server** address.

 ![Screen capture of Skytap dashboard - bootstrap server address](../Images/lab03-workload7.png)

15. Paste this address in to the editor as the value for `bootstrap.servers`.

 ![Screen capture of Skytap dashboard - gedit window](../Images/lab03-workload8.png)

16. Go back to the **Topic connection** page and, under **Certificates**, click the icon to download the **Java truststore**.

 ![Screen capture of Skytap dashboard - Java truststore](../Images/lab03-workload9.png)

17. Choose **Save file**, and then enter the full pathname of the file in to the editor as the value for `ssl.truststore.location`. 

 ![Screen capture of Skytap dashboard - save file](../Images/lab03-workload10.png)

 In this case, the pathname is `/home/student/Downloads/es-cert.jks`.
 
18. Back on the Topic connection page, under **API key**, enter **es-producer** for the application name, and click **Produce only.**

 ![Screen capture of Skytap dashboard - es-producer](../Images/lab03-workload11.png)

19. Click **Generate API key**.

 ![Screen capture of Skytap dashboard - generate API key](../Images/lab03-workload12.png)

20. Click the icon to copy the API key.

 ![Screen capture of Skytap dashboard - copy API key](../Images/lab03-workload13.png)

21. Paste the API key in to the editor as the value for password. Paste between the double quotations marks.

 ![Screen capture of Skytap dashboard - paste API key](../Images/lab03-workload14.png)

22. Save and close the `producer.config` file.

23. In the Event Streams console, click the **X** on the Topic connection page to close it. 

## Step 2. Run the application with load

1. In a command terminal window, in the directory where you saved the es-producer.jar file (/home/student/Downloads), run the following command:

 `java -jar es-producer.jar -t eslab -s small`
 
 This command specifies `eslab` for the Topic, and a predefined `small` size load. 
 
 The output scrolls by very quickly, and then concludes with a message that reports the number of messages sent and some details about performance. 
 
 ![Screen capture of Skytap dashboard - command output](../Images/lab03-workload15.png)
 
2. Go back to the Event Streams console and click the **Monitor** tab.

 ![Screen capture of Skytap dashboard - Monitor tab](../Images/lab03-workload16.png)

 Here you see some metrics for the small load. Scroll down to see all the information that is available. The data refreshes every few seconds. You learn more about monitoring later in this course. 
 
3. Run the test again, but this time with a larger load. In a command terminal window, run the following command:

 `java -jar es-producer.jar -t eslab -s large`
 
4. Go back to the **Monitor** tab in the Event Streams console and notice what happens while the test runs. Notice the differences between running the small load and the large load. 

 If you want, you can also go back to the previous lab and run the starter application (consumer) again, and monitor the results in the console. 
 
 
### End of exercise