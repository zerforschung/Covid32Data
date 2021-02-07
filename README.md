# Cov32 Data

This is a data collection of [Covid19 Exposure Notification Protocol](https://en.wikipedia.org/wiki/Exposure_Notification) data, collected in Berlin subway between mid november 2020 to early january 2021.

Informaiton about the collection process is documented [in our blog](https://zerforschung.org/posts/auf-der-suche-nach-corona-im-berliner-untergrund/). This article also contains some baisc analytics and information about data quality.

## Data format

The dataset contains an array of frames. Each frame represents a mesurement of Exposure Notification Beacons. Mesurements where taken for 2 seconds every minute. There are exceptions in this interval, when we detected, that the Train was parked in a tunnel or depot. We also collected BSSIDs of Wifi networks to calculate locations of the mesurements. For privacy reasons, we don't publish the BSSIDs but the calculated geolocations. For the same reason we don't publish the received beacon data but the result of the key matching, including the associated metadata of a positive keymatch. Also the number of non matching beacons per frame.

Example Frame:

```
{
  "id": 195605, // uniqe id of the frame
  "client_id": 46, // id of the sensor
  "timestamp": "2020-12-28T11:44:55Z", // timestamp in UTC
  "beacon_count": 3, // number of total Exposure Notification Beacons received in this mesurement
  "lat": 52.5149664, // geocoordinates in WGS84, where available
  "lng": 13.4183284,
  "positives": 1, // number of beacons later identified as covid19 positive in the key matching process
  "positive_key_infos": [ // metadata from the positive beacons
    {
      "key_published": "2020-12-30", // Date when this key was published on the RKI keyserver
      "rssi": -92, // signal strength of the BLE beacon
      "risk_level": 7, 
      "days_since_onset_of_symptoms": 1,
      "keyid": 40 // ID of the day key which matched the beacon
    }
  ]
 }
 ```



## Data Quality

As decripted in the article the data has some major flaws:

* It's not enought data
* December was not an ideal time to collect data, because of holliday, change of lockdown rules, low PCR-Test coverage during a high covid incidence period.
* Sensors where not evenly distributed over the subway routes of berlin
* opening of a new subway line during this period
* Sensors where placed in different locations of the trains, also because of different types of trains