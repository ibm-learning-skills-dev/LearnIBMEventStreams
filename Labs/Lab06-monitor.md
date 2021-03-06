# Lab 6: Monitoring Event Streams with IBM Cloud Private

**Duration:** 20 minutes

The Event Streams console provides monitoring capabilities from a Kafka perspective. IBM Cloud Private includes the ELK (Elasticsearch, Logstash, and Kibana) stack, which provides an extensive monitoring and logging framework. 

In this exercise, you explore some of those capabilities. This lab is only intended to provide a brief introduction to the tools. For more information, visit the [IBM Cloud Private Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.1/manage_metrics/logging_elk.html).

## Step 1. Explore the Grafana dashboard

Grafana is an open platform for analytics and monitoring that is included with IBM Cloud Private. In this part of the exercise, you explore the Grafana dashboard for Event Streams. You can use this dashboard to explore Kafka metrics for your Event Streams applications. 

1. Get the Grafana dashboard for Event Streams from GitHub. 

 `https://github.com/IBM/charts/blob/master/stable/ibm-eventstreams-dev/ibm_cloud_pak/pak_extensions/dashboards/ibm-eventstreams-grafanadashboard.json`
 
2. Copy the contents of the file to the clipboard. 
 
3. In the IBM Cloud Private console, select **Platform > Monitoring** from the menu.

 The Grafana dashboard opens in another browser tab.
 
4. In the Grafana dashboard, click **+** (Create) and select **Import**.

5. Paste the code into the **Or paste JSON** field, and click **Load**.

 ![Screen capture of Grafana dashboard - Import screen](../Images/lab05-monitor1.png)
 
6. Click **Import**.

 ![Screen capture of Grafana dashboard - IBM Event Streams dashboard](../Images/lab05-monitor4.png)
 
 The **IBM Event Streams** dashboard displays. Make sure that the **es** namespace and **eslab** release are selected. Feel free to explore the dashboard. You can customize the information that you see in this dashboard. 
 
7. Click **Add Panel** at the top of the page.

 ![Screen capture of Grafana dashboard - Add panel button](../Images/lab05-monitor5.png)

8. Click **Graph**.

 ![Screen capture of Grafana dashboard - Add panel screen](../Images/lab05-monitor6.png)

 A new empty panel displays. 
 
9. Click the title of the new panel and select **Edit**.

10. In the first query field that opens, start typing "kafka" and a list of Kafka metrics is displayed in a drop-down menu. 

 ![Screen capture of Grafana dashboard - Kafka metrics](../Images/lab05-monitor7.png)

11. Select the metric shown here, and click the return arrow in the upper right corner to view it in the panel. 

 ![Screen capture of Grafana dashboard - return arrow](../Images/lab05-monitor8.png)
 
12. Click the **General** tab, enter a name for the panel, and then click the return arrow again.

 ![Screen capture of Grafana dashboard - general tab](../Images/lab05-monitor9.png)

 ![Screen capture of Grafana dashboard - naming the panel](../Images/lab05-monitor10.png)
 
13. Continue to explore the Grafana interface. When finished, close the Grafana browser tab. 

## Step 2. View logs in Kibana

Kibana is an open source data visualization plugin for Elasticsearch, and is included in IBM Cloud Private. You can use it to view log data in various graphical forms. 

If you view a component in the IBM Cloud Private console and select a link within that context, the console displays log data for that particular component. Otherwise, you can build your own queries in the Kibana Discover dashboard. 

### A. View logs for a specific component

In this example, you view log data for a specific pod (container) in Event Streams.

1. In the IBM Cloud Private console, select **Workloads > Helm Releases > eslab**.

2. Scroll down to the list of pods and click the **View logs** link for any one of the pods.

 The Kibana Discover dashbaord opens in a new browser tab. If it says there is no data to display, close the tab, and choose a different pod from the list. 
 
 NOTE: An index pattern, **logstash-\***, was already configured for Kibana in your lab environment. The index pattern tells Kibana what Elasticsearch indices to run against. If this was the first time Kibana was accessed, you would be prompted to set up an index pattern. Kibana requires at least one index pattern to be set up. 
 
3. Click the time range selector tab.

 ![Screen capture of Kibana dashboard - time range selector tab](../Images/lab05-monitor11.png)

 Here, you can select the time range of data to display. Click the tab again to close it.
 
4. Click the arrow next to a log entry to expand it.

 ![Screen capture of Kibana dashboard - expanded log entry](../Images/lab05-monitor12.png)

 The fields for the log entry are shown. These fields can be used in a search filter expression to reduce the returned data, or to search forspecific entries. The log information is derived from the stdout or stderr stream. 

5. To filter the output according to stream, click **Add a filter**.

 ![Screen capture of Kibana dashboard - Add a filter button](../Images/lab05-monitor13.png)
 
6. Under **Filter**, select **stream > is**, enter **stderr** in the field, and click **Save**.

 ![Screen capture of Kibana dashboard - adding a filter](../Images/lab05-monitor14.png)

 The results, if any, are displayed. Feel free to experiment by adding different filters. When finished, close the Kibana browser tab. 

### B. Build a custom query

In this example, you build a custom log query by using the Kibana interface. 

1. In the IBM Cloud Private console, select **Platform > Logging** from the menu.

 Kibana opens in a new browser tab. In this case, it displays all the log data that is available. 

2. In the list of **Available fields**, click any field. For example, click **stream**.

 ![Screen capture of Kibana dashboard - Available fields](../Images/lab05-monitor15.png)

 Details about how records are distributed between the two streams are shown. Feel free to explore the available fields. If you click **Add** next to a field in the list, Kibana sorts the data according to that field. 

3. Build a filter expression based on one or more fields of your choice to reduce the returned data. For example, try adding the filter for stderr, as you did in a previous step. 

4. When you are finished exploring the Kibana interface, close the browser tab.

## Step 3. Metering

1. In the IBM Cloud Private console, select **Platform > Metering** from the menu.

 The metering groups display.
 
2. Under Groups, select **Workloads > es**.

3. In the middle column, enter "kafka" in the search field to see a list of Event Streams Kafka containers.

 ![Screen capture of ICP console metering - kafka resources](../Images/lab05-monitor16.png)

4. Click a container to view usage details in the column on the right. 

 ![Screen capture of ICP console metering - select component](../Images/lab05-monitor17.png)
 
 NOTE: You can export this information by clicking the **Export to CSV**.

5. Click **Details** to view information about the deployed configuration (Software) and operating system (Environment).

 ![Screen capture of ICP console metering - component details](../Images/lab05-monitor18.png)

 NOTE: To obtain a full report, you can click **Download Report** in the upper right corner. 
 
6. When you are finished exploring, you can close the browser.

### End of exercise
<!--June 2019 Edition

**Notices**

This information was developed for products and services offered in the US.
IBM may not offer the products, services, or features discussed in this document in other countries. Consult your local IBM representative for information on the products and services currently available in your area. Any reference to an IBM product, program, or service is not intended to state or imply that only that IBM product, program, or service may be used. Any functionally equivalent product, program, or service that does not infringe any IBM intellectual property right may be used instead. However, it is the user's responsibility to evaluate and verify the operation of any non-IBM product, program, or service.
IBM may have patents or pending patent applications covering subject matter described in this document. The furnishing of this document does not grant you any license to these patents. You can send license inquiries, in writing, to:
IBM Director of Licensing IBM Corporation
North Castle Drive, MD-NC119 Armonk, NY 10504-1785
United States of America
INTERNATIONAL BUSINESS MACHINES CORPORATION PROVIDES THIS PUBLICATION "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
NON-INFRINGEMENT, MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. Some jurisdictions do not allow disclaimer of express or implied warranties in certain transactions, therefore, this statement may not apply to you.
This information could include technical inaccuracies or typographical errors. Changes are periodically made to the information herein; these changes will be incorporated in new editions of the publication. IBM may make improvements and/or changes in the product(s) and/or the program(s) described in this publication at any time without notice.
Any references in this information to non-IBM websites are provided for convenience only and do not in any manner serve as an endorsement of those websites. The materials at those websites are not part of the materials for this IBM product and use of those websites is at your own risk.
IBM may use or distribute any of the information you provide in any way it believes appropriate without incurring any obligation to you.
Information concerning non-IBM products was obtained from the suppliers of those products, their published announcements or other publicly available sources. IBM has not tested those products and cannot confirm the accuracy of performance, compatibility or any other claims related to non-IBM products. Questions on the capabilities of non-IBM products should be addressed to the suppliers of those products.
This information contains examples of data and reports used in daily business operations. To illustrate them as completely as possible, the examples include the names of individuals, companies, brands, and products. All of these names are fictitious and any similarity to actual people or business enterprises is entirely coincidental.
**Trademarks**
IBM, the IBM logo, and ibm.com are trademarks or registered trademarks of International Business Machines Corp., registered in many jurisdictions worldwide. Other product and service names might be trademarks of IBM or other companies. A current list of IBM trademarks is available on the web at “Copyright and trademark information” at www.ibm.com/legal/copytrade.shtml.
**© Copyright International Business Machines Corporation 2019.
This document may not be reproduced in whole or in part without the prior written permission of IBM.**
US Government Users Restricted Rights - Use, duplication or disclosure restricted by GSA ADP Schedule Contract with IBM Corp.

**Trademarks**

The reader should recognize that the following terms, which appear in the content of this training document, are official trademarks of IBM or other companies:IBM, the IBM logo, and ibm.com are trademarks or registered trademarks of International Business Machines Corp., registered in many jurisdictions worldwide.
The following are trademarks of International Business Machines Corporation, registered in many jurisdictions worldwide:
IBM Cloud™
z/OS®Java™ and all Java-based trademarks and logos are trademarks or registered trademarks of Oracle and/or its affiliates.VMware is a registered trademark or trademark of VMware, Inc. or its subsidiaries in the United States and/or other jurisdictions.Other product and service names might be trademarks of IBM or other companies.-->
