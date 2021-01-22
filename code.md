


Import Pacakges:
from pyspark.sql import SparkSession
from pyspark.sql.types import StructType,StructField, StringType, IntegerType,BooleanType,TimestampType,FloatType

Schema Conversion:
data=StructType([\
StructField("ID",StringType(),True),\
StructField("Source",StringType(),True),\
StructField("TMC",IntegerType(),True),\
StructField("Severity",IntegerType(),True),\
StructField("Start_Time",TimestampType(),True),\
StructField("End_Time",TimestampType(),True),\
StructField("Start_Lat",FloatType(),True),\
StructField("Start_Lng",FloatType(),True),\
StructField("End_Lat",FloatType(),True),\
StructField("End_Lng",FloatType(),True),\
StructField("Distance(mi)",FloatType(),True),\
StructField("Description",StringType(),True),\
StructField("Number",IntegerType(),True),\
StructField("Street",StringType(),True),\
StructField("Side",StringType(),True),\
StructField("City",StringType(),True),\
StructField("County",StringType(),True),\
StructField("State",StringType(),True),\
StructField("Zipcode",IntegerType(),True),\
StructField("Country",StringType(),True),\
StructField("Timezone",StringType(),True),\
StructField("Airport_Code",StringType(),True),\
StructField("Weather_Timestamp",TimestampType(),True),\
StructField("Temperature(F)",FloatType(),True),\
StructField("Wind_Chill(F)",FloatType(),True),\
StructField("Humidity(%)  ",FloatType(),True),\
StructField("Pressure(in)",FloatType(),True),\
StructField("Visibility(mi)",FloatType(),True),\
StructField("Wind_Direction ",StringType(),True),\
StructField("Wind_Speed(mph)",FloatType(),True),\
StructField("Precipitation(in)",FloatType(),True),\
StructField("Weather_Condition",StringType(),True),\
StructField("Amenity ",BooleanType(),True),\
StructField("Bump",BooleanType(),True),\
StructField("Crossing",BooleanType(),True),\
StructField("Give_Way",BooleanType(),True),\
StructField("Junction",BooleanType(),True),\
StructField("No_Exit",BooleanType(),True),\
StructField("Railway",BooleanType(),True),\
StructField("Roundabout",BooleanType(),True),\
StructField("Station",BooleanType(),True),\
StructField("Stop",BooleanType(),True),\
StructField("Traffic_Calming ",BooleanType(),True),\
StructField("Traffic_Signal",BooleanType(),True),\
StructField("Turning_Loop",BooleanType(),True),\
StructField("Sunrise_Sunset ",StringType(),True),\
StructField("Civil_Twilight  ",StringType(),True),\
StructField("Nautical_Twilight",StringType(),True),\
StructField("Astronomical_Twilight",StringType(),True),\
])


Read_csv_file:
df_with_schema = spark.read.format("csv").option("header", True).schema(data).load("ProjectData/US_Accidents_June20.csv")
df_with_schema.printSchema()

How to drop the columns
df=df_with_schema.drop('columnname')
df.show()
df=df.drop("TMC","Source","End_Lat","End_Lng","Number","Wind_")




ID
SOURCE
SEVERITY
START-TIME
END-TIME
START-LAT
START-LNG
DISTANCE
STREET
SIDE
CITY
COUNTY
STATE
ZIPCODE
COUNTRY



Replace nan with mean

from pyspark.sql.functions import mean

mean_val=df.select(mean(df.Sales)).collect()

df.na.fill(mean_sales,subset=['Sales']).show()

Rename a column name

df=df.withColumnRenamed("Pressure(in)","Pressure")


df=df.withColumn("zipcode",split(df["Zipcode"],'-').getItem(0))
df.select("zipcode").show()

































