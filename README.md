# Phantom-ROV-Hypack-Data-Processing-
These R scripts provide the means to process the various sensors on the Phantom from the Hypack and ASDL log files into a 1 Hz time series .CSV file.

There are 5 primary scripts that are part of this repository:

**1_Hypack_Data_Parser_Phantom.R**

This script reads in Hypack. RAW files and extracts all collected data readings, it builds a 1 Hz times series of the sensor data logged by Hypack during the survey, and converts position data from a projected coordinate reference system (UTM North Zones, 8 9 or 10) to an unprojected data set of latitude and longitude as decimal degrees. No interpolation of missing values is done at this stage.

The script will try to find depth and position data records for a user defined 'preferred' depth and position source from the Phantom ROV -- in practice, this is likely the more accurate depth of the CTD (rather than the vehicle's onboard sensor) and whatever transponder or responder was used during the survey that is being processed.

This scripts creates on file for each transect (can be multiple transects in a single dive), and write these to seperate .CSV files.

**2_ASDL_Data_Parser_Phantom.R**

This script reads in the log files generated by Advanced Serial data logger. Various cleaning steps are completed on the log files, and daily/hourly log files are aggregated into one "Master" log file for each device that spans the duration of the entire survey/cruise. For all log files, timestamps are generated to match the standard R POSIX timestamp format of YYYY-MM-DD HH:MM:SS, and any duplicate values where the readings occur more frequently than 1 Hz are removed. Master files are generated as .CSV files, one per device/sensor.
