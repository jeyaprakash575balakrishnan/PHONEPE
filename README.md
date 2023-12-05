"C:\Users\91978\Downloads\images.png"

# Data Visualization and Exploration : A User-Friendly Tool Using Streamlit and Plotly

# What is PhonePe Pulse?
  The [PhonePe Pulse website](https://www.phonepe.com/pulse/explore/transaction/2022/4/) showcases more than 2000+ Crore transactions by consumers on an interactive map of India. With over 45% market share, PhonePe's data is representative of the country's digital payment habits.
The insights on the website and in the report have been drawn from two key sources - the entirety of PhonePe's transaction data combined with merchant and customer interviews. The report is available as a free download on the [PhonePe Pulse website](https://www.phonepe.com/pulse/explore/transaction/2022/4/) and [GitHub](https://github.com/PhonePe/pulse).

# Libraries/Modules needed for the project!

 1. Plotly - (To plot and visualize the data)
 2. Pandas- (To Create a DataFrame with the scraped data)
 3. mysql.connector - (To store and retrieve the data)
 4. Streamlit- (To Create Graphical user Interface)
 5. json - (To load the json files)

### Step 1:
 
 **Importing the Libraries:**
 
   Importing the libraries. As I have already mentioned above the list of libraries/modules needed for the project. First we have to import all those libraries. If the libraries are not installed already use the below piece of code to install.

        !pip install ["Name of the library"]
    
   If the libraries are already installed then we have to import those into our script by mentioning the below codes.

        import pandas as pd
        import pymysql
        import streamlit as st
        import plotly.express as px
        import os
        import json
        from streamlit_option_menu import option_menu
        from PIL import Image
        
 ### Step 2:
 
 **Data extraction:** 

   Clone the Github using scripting to fetch the data from the Phonepe pulse Github repository and store it in a suitable format such as JSON. Use the below syntax to clone the phonepe github repository into your local drive.
    
        from git.repo.base import Repo
        Repo.clone_from("GitHub Clone URL","Path to get the cloded files")
      
 ### Step 3:
 
 **Data transformation:**
 
   In this step the JSON files that are available in the folders are converted into the readeable and understandable DataFrame format by using the for loop and iterating file by file and then finally the DataFrame is created. In order to perform this step I've used **os**, **json** and **pandas** packages. And finally converted the dataframe into CSV file and storing in the local drive.

    path1 = "Path of the JSON files"
    agg_trans_list = os.listdir(path1)

    # Give any column names that you want
    columns1 = {'State': [], 'Year': [], 'Quarter': [], 'Transaction_type': [], 'Transaction_count': [],'Transaction_amount': []}
    
    
Looping through each and every folder and opening the json files appending only the required key and values and creating the dataframe.

 ### Step 4:
 
 **Database insertion:**
 
   To insert the datadrame into SQL first I've created a new database and tables using **"mysql-connector-python"** library in Python to connect to a MySQL database and insert the transformed data using SQL commands.
   
   **Creating the connection between python and mysql**
   
mydb = pymysql.connect(host = '127.0.0.1',user='root',passwd='Jeya@123',database = "phonepe")
mycursor = mydb.cursor()

**Creating tables**
mycursor.execute("create table agg_trans (State varchar(100), Year int, Quarter int, Transaction_type varchar(100), Transaction_count int, Transaction_amount double)")

for i,row in agg_trans.iterrows(): 

    sql = "INSERT INTO agg_trans VALUES (%s,%s,%s,%s,%s,%s)"
    mycursor.execute(sql, tuple(row))
    mydb.commit()

 ### Step 5:
 
 **Dashboard creation:**
 
   To create colourful and insightful dashboard I've used Plotly libraries in Python to create an interactive and visually appealing dashboard. Plotly's built-in Pie, Bar, Geo map functions are used to display the data on a charts and map and Streamlit is used to create a user-friendly interface with multiple dropdown options for users to select different facts and figures to display.


THE MAIN COMPONENTS OF DASHBOARD ARE

    1 GEO-VISUALIZATION
    
    2 TRANSACTIONS ANALYSIS
    
    3 USERS ANALYSIS
    
    4 TOP STATES DATA

**Conclusion**

We have successfully collected and processed large volumes of data related to PhonePe's usage, transactions, and user demographics. By presenting data in a visual and informative manner, this project has enabled us to understand and communicate valuable information to stakeholders, users, and decision-makers.
    

  
