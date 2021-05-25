# DatabricksTraining
# Lab from 5.25 Data and AI

# File location and type
file_location = "/FileStore/tables/Labs.dbc"
file_type = "dbc"

# CSV options
infer_schema = "false"
first_row_is_header = "false"
delimiter = ","

# The applied options are for CSV files. For other file types, these will be ignored.
df = spark.read.format(file_type) \
  .option("inferSchema", infer_schema) \
  .option("header", first_row_is_header) \
  .option("sep", delimiter) \
  .load(file_location)

display(df)

# Create a view or table

temp_table_name = "Labs_dbc"

df.createOrReplaceTempView(temp_table_name)

%sql

/* Query the created temp table in a SQL cell */

select * from `Labs_dbc`

# With this registered as a temp view, it will only be available to this particular notebook. If you'd like other users to be able to query this table, you can also create a table from the DataFrame.
# Once saved, this table will persist across cluster restarts as well as allow various users across different notebooks to query this data.
# To do so, choose your table name and uncomment the bottom line.

permanent_table_name = "Labs_dbc"

# df.write.format("parquet").saveAsTable(permanent_table_name)
