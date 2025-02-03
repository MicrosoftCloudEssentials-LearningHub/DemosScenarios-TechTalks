# Fabric known errors - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-02-03

----------

> [!IMPORTANT]
> Here is a brief overview of error messages and their solutions.

## Don't have access 

```
You don't have access to this content
Please try again later or contact support. If you contact support, please provide these details
```

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/8ad0d196-d4ee-4b47-8345-01d9c71dccdd" />
</p>

> [!TIP]
> Please ensure that the user is granted the appropriate permissions, whether it be for the workspace, app, or the report itself.

## Cannot load model

```
Couldn't load the model schema associated with this report. Make sure you have a connection to the server, and try again.
Please check the technical details for more information. If you contact support, please provide these details.
```

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/7b824ef0-f4b1-4cfa-af32-89864751bdff" />
</p>

> [!TIP]
> Please ensure your Fabric capacity is on.

## Could not connect to the data source 

```
There was an error communicating with Analysis Services. Please verify that the data source is available and your credentials are correct.

If you contact support, please provide these details.
```

> [!TIP]
> If you encounter these errors, it's necessary to grant the appropriate `(semantic model, sql analytics endpoint, and the app` permissions for access.

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/7361815f-7a53-4ae7-80f9-5bd6e3033b59" />
</p>

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/05fac487-647a-48c2-b2b9-d9f1f0b172ea" />
</p>


   - Let's say you want only `viewer` permissions:

     1. Need to give access to the lakehouse/sql analytics endpoint:
        
        <img width="436" alt="image" src="https://github.com/user-attachments/assets/814f831f-19b8-4939-a3e2-618385c4827b">

        > `Read All SQL Endpoint Data` permission allows users to access and read data from SQL endpoints within the Fabric environment. This permission is typically required for users who need to: <br/>
        > - Query Data: Execute SQL `queries against the data stored in the Fabric environment`. <br/>
        > - Access Reports: `View and interact with reports and dashboards that rely on SQL data sources`. <br/>
        > - Data Analysis: `Perform data analysis and generate insights` using SQL-based data.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/b87137f1-b464-43df-a04d-593a41b3131a">

      2. Make sure the person already have access to the semantic model:

         <img width="550" alt="image" src="https://github.com/user-attachments/assets/f5344f85-53f3-48dc-b0b1-6b3c5995bbd6">

> - Granting `Read, ReadData` access to the `semantic model, sql analytics endpoint` <br/>
> - Grating `App audience` will enable the assigned identity to view it.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/353d88ad-a4a7-4aef-aff4-d584901c29d8">


<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
