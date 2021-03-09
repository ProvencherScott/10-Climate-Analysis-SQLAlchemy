# 10-Climate-Analysis-SQLAlchemy

The main objective of this assignment was to create and run a Flask server using sqlalchemy, execute dynamic database queries with Flask and create routes that call back to the APIs related to Hawaii data. I was able to use the Python SQL toolkit and OJR to create an engine connection to hawaii.sqlite(provided) : 

### engine = create_engine("sqlite:///Resources/hawaii.sqlite")

I created queries to retrieve results related to specific dates and precipitation values. Also, I created a query to retrieve the the total temperature observations within a year range. I created two plots using matplotlib and saved the .png in the images folder. I setup a Flask server in app.py using app = Flask(_name_) which, would be used to connect to each route and display the information live on the server. The **return jsonify()** function was executed to display the jsonified dictionary specific to that route. My API routes are shown below:

The repo consisits of a Jupyter Notebook, main app.py (to establish connection), sqlite file and two csv.

## Hawaii Temperature Analysis:

### Precipitation Analysis:

1. Design a query to retrieve the last 12 months of precipitation data. 2 Select only the date and prcp values.

@app.route("/api/v1.0/precipitation")
def rain():
    session = Session(engine)
    results = session.query(Measurement.date,func.sum(Measurement.prcp)).\
    filter(Measurement.date >= '2016-08-23').\
    group_by(Measurement.date).all()

### Station Analysis:

1. Design a query to find the most active stations. 2. Design a query to retrieve the last 12 months of temperature observation data (TOBS).

@app.route("/api/v1.0/stations")
def stations():
    session = Session(engine)
    results = session.query(Station.station).all()
    
### Most Active Station:

1. Query the dates and temperature observations of the most active station for the last year of data.

@app.route("/api/v1.0/tobs")
def observations():
    session = Session(engine)
    temp_freq = session.query(Measurement.date, Measurement.tobs).\
        filter(Measurement.date >= '2016-08-23').\
        filter(Measurement.station == 'USC00519281').all()
 
 
 ### Temperature JSON List:
 
 1. List of the minimum temperature, the average temperature, and the max temperature for a given start or start-end range.

@app.route("/api/v1.0/<start>")
def start_date_only(start):
    search_term = start
    session = Session(engine)
    results = session.query(Measurement.date, func.min(Measurement.tobs),func.max(Measurement.tobs), func.avg(Measurement.tobs)).\
         filter(Measurement.date >= search_term).group_by(Measurement.date).all()


Other imported libraries:

pandas

matplotlib

datetime

numpy

stats

flask

session

automap_base
