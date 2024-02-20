# atMetadata Reference

Each atRecord has associated metadata, this is used both by the atServer and the atClient to treat data as requested. This could be for example a TTL (Time To Live) value after which the whole atRecord is deleted. The full list is [documented ](https://pub.dev/documentation/at\_commons/latest/at\_commons/Metadata-class.html)but here is a sample of the most used properties.

#### Time Til Born (TTB) -milliseconds

The time that this record will be available. This means that the data can be populated early but it will not be available until this time.

#### Time To Live (TTL) -milliseconds

The time that this record will remain available before it is deleted.

#### Time To Refresh (TTR) - seconds

The time interval to automatically refresh data from the owners atServer.

#### isPublic -boolean

Not all records need to be encrypted, public records are not encrypted but are signed by the owning atSign.

