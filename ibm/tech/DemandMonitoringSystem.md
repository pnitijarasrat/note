# Demand Request and Handling System

## Objective of this System

- To request demand and other factors ( late, defect, missing ) from Advisory Board.
- To insert data into database for other department.
- To calculate and monitor all demand for every branch to operator.
- To make a report/summary of sale for marketing and finance

## Tech Use

- Frontend: React
- Backend: Node [don't need anymore]
- Database: Google Firestore

## Components

API

- [GET](https://ibmapi.onrender.com/Demand/) / How to [cache](https://www.robinwieruch.de/local-storage-react/#local-storage-in-react) data

Data Structure

- {"day" , "A", "B", "C", "D", etc}

## Hierarchy

- Get demand every day ( in ibm ) and cache it every get call
- Pass all demand via props ( to monitor and data pages )

## Page

- Monitor Page ( show demand of each branch )
- Data page ( for other department who want to use data )

## To Do

Not Done

- [ ] Backend Handle storing data
- [ ] Handle Promotion
- [ ] Handle Sync Function

Done

- [x] Add Sync Demand Button
- [x] Add increase and decrease button
- [x] Data Export Page

## To Revise

- Connect with API both request and storing and downloading data
- CORS Policy from backend
