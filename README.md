# Admob-Play_GDS

<h1> Process for Creating App Dashboards </h1>
The below documentation demonstrates how to retrieve data from the AdMob API using a custom Google Data Studio (GDS) connection, built with Google Apps Script (GAS), connect to Play Console data using the Google BigQuery (GBQ) Data Transfer Service, generate extracts of these feeds, and generate realtime App acquisition, retention, and monetization performance dashboards in GDS.

<h2> Building the AdMob API Connection </h2>
  
  1. Create a new project in GAS (https://script.google.com/home)
  2. Clear the code from *Code.gs*
  3. Enter the code from *AdMob-GAS-x* within the main section of this Git repository
  4. Navigate to your Google Cloud Platform (GCP) instance (https://console.cloud.google.com/home/)
  5. Enable the AdMob API by searching AdMob API from the search bar, clicking *AdMob API*, and once at the marketplace screen for the API, clicking enable
  6. Once the API is enabled, within GCP navigate to APIs & Services \> Credentials
  7. Generate new OAuth 2.0 credentials
    
    * Allow GDS (https://datastudio.google.com) and GAS (https://script.google.com) Javascript origins
    * Allow your GAS project(s) as authorized redirect URI(s) (https://script.google.com/macros/d/**your-project**/usercallback and (https://script.google.com/macros/s/**your-project**/exec)

  8. Once the credentials are created, input client ID and client secret information from the OAuth credentials generated
  9. Within your GAS project, navigate to the *view* menu, select 'show manifest file'
  10. Update the manifest file with JSON information from *GAS-Manifest* within the main section of this Git repository
  11. Once this is done navigate to the *publish* menu within your GAS project and select *deploy from manifest*

<h2> Configuring the BigQuery Data Transfer Service </h2>
  
  1. Navigate to your GCP instance (https://console.cloud.google.com/home/)
  2. Search for the BigQuery, BigQuery Connection, and BigQuery Data Transfer Service APIs and enable them from the marketplace
  3. Navigate to the BigQuery console by searching BigQuery in the search bar
  4. Select *Data Transfers* from the left-side menu
  5. Choose create transfer and select 'Google Play' as the source
  6. Configure the destination as desired and save the transfer configuration (note that a dataset must already be created for the transfer to be delivered to)
  7. Once the transfer service has been configured, Play Console datasets should be available from the SQL workspace view within BigQuery
  8. To create views of installs and app revenue by Country, create a new view using the code *BQ-Installs-Earnings* from the main section of this Git repository

<h2> Connecting to the AdMob GAS Custom Connector in GDS </h2>
  
  1. Navigate to GDS (https://datastudio.google.com/)
  2. Select *Data Sources* \> *Create* \> *Data Source*
  3. Choose the custom connector built in GAS under Partner Connectors and configure using the appropriate AdMob Publisher ID and date range
  4. Click '*Connect*'


<h2> Connecting to BigQuery Play Console Data in GDS </h2>
  
  1. Navigate to GDS (https://datastudio.google.com/)
  2. Select *Data Sources* \> *Create* \> *Data Source*
  3. Choose the BigQuery connection within the Google Connectors section
  4. Navigate to the Project, Dataset, and Table/View which you want to connect to
  5. Click '*Connect*'

<h2> Creating Extracts of Live Data Sources in GDS </h2>
Extracts are good for minimizing dashboard load times as well as reducing the volume of data processed (and associated costs) when dashboards are updated or queried

  1. Navigate to GDS (https://datastudio.google.com/)
  2. Select *Data Sources* \> *Create* \> *Data Source*
  3. Choose the Extract Data connection within the Google Connectors section
  4. Select the data source for which you want to create the extract
  5. Configure the extract by choosing the dimensions, metrics, and date range desired
  6. Set a refresh cadence for your extract by choosing the cadence and timing from the dialogue box on the lower right-hand side of the configuration window
