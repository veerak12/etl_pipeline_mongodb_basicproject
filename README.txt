# ETL_pipeline_mongodb_basicproject


Step-by-Step Process and Description for the Given Code:

1.Import necessary libraries:
  The code begins by importing the required libraries:
  Faker library is imported to generate fake data for the sales records.
  random library is imported to generate random values for quantity and price.
  pymongo library is imported to interact with the MongoDB database.
  json library is imported to work with JSON data.

2.Initialize Faker object:
  The code creates a Faker object named fake. This object will be used to generate fake data for the sales records.

3.Define the generate_fake_sales_data() function:
  This function takes an argument num_records representing the number of sales records to generate.
  Inside the function, an empty list data is created to store the generated records.
  A for loop is used to generate num_records sales records.
  For each record, a dictionary is created with the following fields:
    'customer_name': A randomly generated fake name using fake.name().
    'product_name': A randomly generated fake word using fake.word().
    'quantity': A random integer between 1 and 100 using random.randint().
    'price': A random float between 10 and 100 rounded to 2 decimal places using random.uniform() and round().
  Each record is appended to the data list.
  Finally, the data list is returned.

4.Define the load_data_to_mongodb() function:
  This function takes a single argument data representing the sales records to be loaded into the MongoDB database.
  Inside the function, a MongoClient object is created with the connection string 'mongodb://localhost:27017/'.
  The MongoClient object is then used to connect to the MongoDB server.
  A database named 'sales_db' is accessed using the client['sales_db'] syntax.
  A collection named 'sales_collection' is accessed using the db['sales_collection'] syntax.
  The insert_many() method is called on the collection object to insert multiple documents (sales records) into the collection.
  The data list is passed as an argument to the insert_many() method to insert all the sales records into the collection.

5.Define the extract_details_from_mongodb() function:
  This function does not take any arguments.
  Inside the function, a MongoClient object is created with the connection string 'mongodb://localhost:27017/'.
  The MongoClient object is then used to connect to the MongoDB server.
  A database named 'sales_db' is accessed using the client['sales_db'] syntax.
  A collection named 'sales_collection' is accessed using the db['sales_collection'] syntax.
  A MongoDB aggregation pipeline is defined using the $group and $sort stages.
  The $group stage groups the documents by 'customer_name', calculates the total quantity and total price for each customer using the $sum and $multiply operators respectively, and     
   stores the results in the fields 'total_quantity' and 'total_price'.
  The $sort stage sorts the grouped documents in descending order based on the 'total_price' field.
  The pipeline is passed to the aggregate() method of the collection object to execute the aggregation and retrieve the results.
  The extracted details are printed to the console using a for loop.

6.Define the etl_pipeline() function:
  This function takes a single argument num_records representing the number of sales records to generate and process.
  Inside the function, the generate_fake_sales_data() function is called to generate fake sales data.
  The generated data is then passed to the load_data_to_mongodb() function to load the data into the MongoDB database.
  Finally, the extract_details_from_mongodb() function is called to extract the required details from the MongoDB database.

7.Run the ETL pipeline:
The code outside the function definitions calls the etl_pipeline() function with an argument of 1000 to run the ETL pipeline with 1000 records.
