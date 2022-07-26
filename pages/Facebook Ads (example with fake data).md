project_name:: [[Data_sources]] 
status:: #Draft 
type:: #internal 
assign:: [[Dmitry Korzhov]]

- TODO Do this page better [[Dmitry Korzhov]]
	- TODO sure, I'll try it today.
		- TODO I understand, good [[Dmitry Korzhov]]
- ## Nagivation
	- ((62c742a5-d636-4417-a14d-6bda24720a84))
	- ((62c742e4-fdcb-4a5d-a2d7-6ae371b357eb))
	- ((62c742f6-78e6-4c04-b001-b0c545759fbe))
	- ((62c7431e-210b-4d8b-a92f-fd9e37ece95c))
	- ((62c74411-32e2-4e39-8f4e-4fdd94381f09))
- ## General and integration description
  id:: 62c742a5-d636-4417-a14d-6bda24720a84
	- Facebook Ads provides a history of the settings of your Ad Account, Campaigns, Ad Sets, Ads, and Ad Creatives. Facebook Ads also fetches Ad Insights data.
	- Stitch’s Facebook Ads integration replicates ad, campaign, and adcreative data using the [Facebook Marketing API 10.0](https://developers.facebook.com/docs/marketing-apis).
	- See [Facebook documentation](https://developers.facebook.com/docs/marketing-api/reference) for more information.
## Features
id:: 62c742e4-fdcb-4a5d-a2d7-6ae371b357eb
	- A high-level look at Stitch's Facebook Ads (v1) integration, including release status, useful links, and the features supported in Stitch.
	- | FEATURE NAME                     	| SUPPORTED   	|
	  | API availability                 	| Available   	|
	  | Anchor Scheduling                	| Supported   	|
	  | Table-level reset                	| Supported   	|
	  | Advanced Scheduling              	| Unsupported 	|
	  | Configurable Replication Methods 	| Unsupported 	|
	  | Table selection                  	| Supported   	|
	  | Select all                       	| Supported   	|
	  | Column selection                 	| Supported   	|
	  | Loading Reports                  	| Supported   	|
	  | Extraction Logs                  	| Supported   	|
## Schema information
id:: 62c742f6-78e6-4c04-b001-b0c545759fbe
	- #+BEGIN_PINNED
	  **Data dictionary filtered by specific data source (Embed GDS report at this moment)**
	  #+END_PINNED
	- @@html: <iframe width="650" height="500" src="https://datastudio.google.com/embed/reporting/bc22dac3-e0bc-4135-92dd-e056ebf9d234/page/9Y3YB" frameborder="0" style="border:0" allowfullscreen></iframe>@@
	- This schema applies to all Facebook Ads connectors.
	  collapsed:: true
		- ![Facebook Ads ERD.png](../assets/Facebook_Ads_ERD_1657319574502_0.png){:height 474, :width 746}
- ## Setup guide
  id:: 62c7431e-210b-4d8b-a92f-fd9e37ece95c
	- To set up Facebook Ads in Stitch, you need:
	- **Verify your access in Facebook Ads.** If the user who creates the integration has restricted permissions - meaning the user doesn’t have access to all campaigns or ads - Stitch may encounter issues replicating data.
	- Even if you only intend to sync certain pieces of data post-setup, the user completing the initial setup should still have full access.
	- **Pause all ad-blocking software currently in use.** Because Facebook authentication uses pop ups, you may encounter issues if ad blockers aren’t disabled during the setup.
	- ### Step 1: Add Facebook Ads as a Stitch data source    [](https://www.stitchdata.com/docs/integrations/saas/facebook-ads#add-stitch-data-source)
	  collapsed:: true
		- [Sign into your Stitch account](https://app.stitchdata.com/).
		- On the Stitch Dashboard page, click the **Add Integration** button.
		- Click the **Facebook Ads** icon.
		- Enter a name for the integration. This is the name that will display on the Stitch Dashboard for the integration; it’ll also be used to create the schema in your destination.
		- For example, the name “Stitch Facebook Ads” would create a schema called   `stitch_facebook_ads`   in the destination. **Note**: Schema names cannot be changed after you save the integration.
		- #### Step 1.2: Include deleted data
		  collapsed:: true
			- Check the **Include data from deleted campaigns, ads, and adsets** box to have Stitch replicate data for these deleted objects.
			- **Note**: Data for deleted campaigns, ads, and adsets will be included only in [**Core Object**](https://www.stitchdata.com/docs/integrations/saas/facebook-ads#schema) tables.
		- #### Step 1.1: Select an attribution window
		  collapsed:: true
			- An attribution window is the amount of time for attributing results to ads and the lookback period after those actions occur during which ad results are counted.
			- We recommend selecting the [same attribution window you use in Facebook Ads](https://www.facebook.com/business/help/458681590974355) to prevent discrepancies between Facebook’s UI and data replicated by Stitch. For example: If the attribution window in Facebook Ads is **7 days**, you should define this setting as **7 days**
			- Then, during every replication job, Stitch will replicate **the past seven days’ worth of data** to account for result attribution. This will ensure that records updated during the attribution period are correctly captured by Stitch.
			- For more info, see the [Attribution windows and data extraction](https://www.stitchdata.com/docs/integrations/saas/facebook-ads#attribution-windows-data-extraction) section.
	- ### Step 2: Define the historical replication start date
	  collapsed:: true
		- For tables using **Key-based Incremental Replication**, data **equal to or newer than this date** will be replicated to your destination.
		- For tables using **Full Table Replication**, all data - including records that are older, equal to, or newer than this date - will be replicated to your destination.
		- Change this setting if you want to replicate data beyond Facebook Ads’s default setting of **1 year**. For a detailed look at historical replication jobs, check out the [Syncing Historical SaaS Data](https://www.stitchdata.com/docs/replication/syncing-historical-saas-data-resetting-replication-keys) guide.
		-
	- ### Step 3: Create a replication schedule
	  collapsed:: true
		- In the **Replication Frequency** section, you’ll create the integration’s [replication schedule](https://www.stitchdata.com/docs/replication/replication-scheduling). An integration’s replication schedule determines how often Stitch runs a replication job, and the time that job begins.
		- Facebook Ads integrations support the following replication scheduling methods:
		- [Replication Frequency](https://www.stitchdata.com/docs/replication/replication-scheduling/replication-frequency)
		- [Anchor Scheduling](https://www.stitchdata.com/docs/replication/replication-scheduling/anchor-scheduling)
		- To keep your row usage low, consider setting the integration to replicate less frequently. See the [Understanding and Reducing Your Row Usage guide](https://www.stitchdata.com/docs/getting-started/understanding-stitch-usage) for tips on reducing your usage.
	- ### Step 4: Authorize Stitch to access Facebook Ads
	  collapsed:: true
		- After clicking the **Authorize** button, a small pop-up window will display.
		- You’ll be taken through a series of steps to allow Stitch to access data from your Public Profile, Facebook Ads, and related stats.
		- Click **Okay** to advance through these steps.
		- After you’ve finished authorizing Stitch, you’ll be prompted to select the Facebook Ad Account you want to pull data from. Select the desired account by clicking the checkbox in the **Connect** column.
		- If you don’t see the profiles that you would expect to, verify your Facebook Ads permissions before reaching out to support.
		- Click the **Save Connections** button.
		- After your credentials are validated, you’ll be directed back to Stitch (click the **All Done** button to wrap things up) and the Integration Details page will display.
	- ### Step 5: Set objects to replicate
	  collapsed:: true
		- The last step is to select the tables and columns you want to replicate. [Learn about the available tables for this integration.](https://www.stitchdata.com/docs/integrations/saas/facebook-ads#schema)
		- **Note**: If a replication job is currently in progress, new selections won’t be used until the next job starts.
		- Selection options.
		  collapsed:: true
			- For Facebook Ads integrations, you can select:
			- **Individual tables and columns**
			- **All tables and columns**
			- Click the tabs to view instructions for each selection method.
		- Individual tables and columns.
		  collapsed:: true
			- In the integration’s **Tables to Replicate tab**, locate a table you want to replicate.
			- To track a table, click the **checkbox** next to the table’s name. A blue checkmark means the table is set to replicate.
			- To track a column, click the **checkbox** next to the column’s name. A blue checkmark means the column is set to replicate.
			- Repeat this process for all the tables and columns you want to replicate.
			- When finished, click the **Finalize Your Selections** button at the bottom of the screen to save your selections.
		- All tables and columns.
		  collapsed:: true
			- Click into the integration from the Stitch Dashboard page.
			- Click the **Tables to Replicate** tab.
			- In the list of tables, click the box next to the **Table Names** column.
			- In the menu that displays, click **Track all Tables and Fields**:
			- ![](file:///Applications/Logseq.app/Contents/Resources/assets/select-all-tables-menu_1657197256612_0.png)
			- Click the **Finalize Your Selections** button at the bottom of the page to save your data selections.
	- ### Initial and historical replication jobs
	  collapsed:: true
		- After you finish setting up Facebook Ads, its **Sync Status** may show as **Pending** on either the Stitch Dashboard or in the Integration Details page.
		- For a new integration, a **Pending** status indicates that Stitch is in the process of scheduling the initial replication job for the integration. **This may take some time to complete.**
	- ### Free historical data loads
	  collapsed:: true
		- The first seven days of replication, beginning when data is first replicated, are free. Rows replicated from the new integration during this time won’t count towards your quota. Stitch offers this as a way of testing new integrations, measuring usage, and ensuring historical data volumes don’t quickly consume your quota.
- ## Release Notes
  id:: 62c74411-32e2-4e39-8f4e-4fdd94381f09
	- June 2022
	  collapsed:: true
		- We have upgraded our Facebook Ads connector to version 14.0 of the Facebook API. For more information, see Facebook's [v14.0 changelog](https://developers.facebook.com/docs/graph-api/changelog/version14.0).
		- We have added the following new fields to the   `AD_SET_HISTORY`   table:
		  collapsed:: true
			- `promoted_object_custom_conversion_id`
			- `promoted_object_custom_event_str`
			- `promoted_object_offline_conversion_data_set_id`
			- `promoted_object_pixel_aggregation_rule`
			- `promoted_object_pixel_rule`
			- `promoted_object_retention_days`
		- Learn more in Facebook's [Ad Set, Promoted Object documentation](https://developers.facebook.com/docs/marketing-api/reference/ad-promoted-object/v14.0).
	- January 2022
	  collapsed:: true
		- Now, when you set the **Sync all metadata** toggle to FALSE in the connector setup form, we automatically deselect the corresponding tables on the **Schema** tab and exclude them from syncs. Previously, we did not deselect the tables on the Schema tab.
	- October 2021
	  collapsed:: true
		- Now, during connector setup, if you don't provide the   `business_management`   permission to access the business details fields, the connector setup tests pass with a warning. The warning lists the fields that we’ll skip during the sync. In addition, we generate a warning alert on your Fivetran dashboard. Previously, the setup tests failed without this permission.
		- We have added two new fields,   `approximate_count_lower_bound`   and   `approximate_count_upper_bound`  , to the   `CUSTOM_AUDIENCE_HISTORY`   table.
		- We have removed the   `approximate_count`   field because [it has been deprecated](https://developers.facebook.com/docs/graph-api/changelog/ooc-changes/oct-13-2021#custom-audience).
- ## Questions
  id:: 62c744e6-3e7e-4310-8319-f29ff836a61e
	- We're always happy to help with any other questions you might have! Send us an email.
- ## Feedback form
  id:: 62cad56d-7158-45e1-a5cd-1383e1d31d2d
