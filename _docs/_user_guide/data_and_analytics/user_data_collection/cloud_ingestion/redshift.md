---
nav_title: Redshift
article_title: Braze Cloud Data Ingestion for Redshift
description: "This reference article covers Braze Cloud Data Ingestion and how to sync relevant user data to your Reshift integration."
page_order: 2
page_type: reference

---

# Cloud Data Ingestion for Redshift

{% alert important %}
Braze Cloud Data Ingestion for Redshift is currently in early access. Contact your Braze account manager if you are interested in participating in the early access.
{% endalert %}

## Product setup

New Cloud Data Ingestion integrations require some setup on the Braze side and in your Redshift instance. Follow these steps to set up the integration:
1. In your Redshift instance, set up the table(s) or view(s) you want to sync to Braze
2. Create a new integration in the Braze dashboard
3. Test the integration and start the sync

### Set up tables or views

#### Step 1: Set up the table 

Optionally, set up a new Database and Schema to hold your source table
```json
CREATE DATABASE BRAZE_CLOUD_PRODUCTION;
CREATE SCHEMA BRAZE_CLOUD_PRODUCTION.INGESTION;
```
Create a table (or view) to use for your CDI integration
```json
CREATE TABLE BRAZE_CLOUD_PRODUCTION.INGESTION.USERS_ATTRIBUTES_SYNC (
   updated_at timestamptz default sysdate,
   external_id varchar,
   payload varchar(max)
)
```

You can name the database, schema, and table as you'd like, but the column names should match the preceding definition.

- `UPDATED_AT` - The time this row was updated in or added to the table. We will only sync rows that have been added or updated since the last sync.
- `EXTERNAL_ID` - This identifies the user you want to update. You can use one of external_id, user_alias, or braze_id.
- `PAYLOAD` - This is a JSON string of the fields you want to sync to the user in Braze.
 
#### Step 2: Create User and grant permissions 

```json
CREATE USER braze_user PASSWORD '{password}';
GRANT SELECT ON TABLE USERS_ATTRIBUTES_SYNC TO braze_user
```

This is the minimum required permissions for this user; if creating multiple CDI integrations, you may want to grant permissions to a schema, or manage permissions using a group. 

#### Step 3: Allow access to Braze IPs (optional) 

If you have a firewall or other network policies in place, you will need to give Braze network access to to your Redshift instance. Allow access from the below IPs that correspond to the region of your Braze dashboard. 

| For Instances `US-01`, `US-02`, `US-03`, `US-04`, `US-05`, `US-06` | For Instances `EU-01` and `EU-02` |
|---|---|
| `23.21.118.191`| `52.58.142.242`
| `34.206.23.173`| `52.29.193.121`
| `50.16.249.9`| `35.158.29.228`
| `52.4.160.214`| `18.157.135.97`
| `54.87.8.34`| `3.123.166.46`
| `54.156.35.251`| `3.64.27.36`
| `52.54.89.238`| `3.65.88.25`
| `18.205.178.15`| `3.68.144.188`
|   | `3.70.107.88`

### Create a new integration in the Braze dashboard

Navigate to the Redshift page on Braze, under **Technology Partners**, and click **Create new import sync**.

1. **Add Redshift connection information and source table**<br>
Input the information for your Redshift data warehouse and source table, then proceed to the next step.<br>![][1]<br><br>
2. **Configure sync details**<br>
Next, choose a name for your sync and input contact emails. We'll use this contact information to notify you of any integration errors (e.g., access to the table was removed unexpectedly).<br>![][2]<br><br> You will also choose the data type and sync frequency. Frequency can be anywhere in the range of every 15 minutes to once per month. We'll use the time zone configured in your Braze dashboard to schedule the recurring sync. Supported data types are Custom Attributes, Custom Events, and Purchase Events and the data type for a sync cannot be changed after creation. 

### Test connection

Once all configuration details for your sync are entered, click **Test connection**. If successful, you'll see a preview of the data. If for some reason we can't connect, we'll display an error message to help you troubleshoot the issue.

![][3]

{% alert note %}
You must successfully test an integration before it can move from Draft into Active state. If you need to close out of the creation page, your integration will be saved, and you can revisit the details page to make changes and test.  
{% endalert %}

### Set up additional integrations or users (optional)

You may set up multiple integrations with Braze, but each integration should be configured to sync a different table. When creating additional syncs, you may reuse existing credentials if connecting to the same Redshift account.
![][4]

If you reuse the same user across integrations, you will not be able to delete the user in the Braze dashboard until it's removed from all active syncs.

### Running the sync

Once activated, your sync will run on the schedule configured during setup. If you want to run the sync outside of the normal schedule for testing or to fetch the most recent data, click **Sync Now**. This run will not impact regularly scheduled future syncs.  
![][5]

[1]: {% image_buster /assets/img/cloud_ingestion/ingestion_6.png %}
[2]: {% image_buster /assets/img/cloud_ingestion/ingestion_7.png %}
[3]: {% image_buster /assets/img/cloud_ingestion/ingestion_8.png %}
[4]: {% image_buster /assets/img/cloud_ingestion/ingestion_9.png %}
[5]: {% image_buster /assets/img/cloud_ingestion/ingestion_10.png %}