AddAsset Method
===============

Create or replace an asset.


Request Format
--------------

+-------------+-------------------------------+---------+--------------------+
| *Parameter* | *Description*                 | *Type*  | *Required*         |
+=============+===============================+=========+====================+
| `AssetID`   | UUID of the asset             | UUID    | Optional           |
+-------------+-------------------------------+---------+--------------------+
| `CreatorID` | UUID of the asset creator     | UUID    | Optional, defaults |
|             |                               |         | to UUID.Zero       |
+-------------+-------------------------------+---------+--------------------+
| `Asset`     | Raw asset data                | Binary  | Yes                |
+-------------+-------------------------------+---------+--------------------+
| `Temporary` | True if this is a temporary   | Boolean | Optional, defaults |
|             | asset                         |         | to False           |
+-------------+-------------------------------+---------+--------------------+
| `Public`    | True if this asset is         | Boolean | Optional, defaults |
|             | publicly accessible (without  |         | to True            |
|             | authorization)                |         |                    |
+-------------+-------------------------------+---------+--------------------+

|

Sample request: ::

    POST /assets/ HTTP/1.1
    Content-Length: 42574
    Content-Type: multipart/form-data; boundary=--AaB03x

    --AaB03x
    Content-Disposition: form-data; name="AssetID"

    f02ed1f6-c1fd-4781-b38a-f337e880f822
    --AaB03x
    Content-Disposition: form-data; name="CreatorID"

    5a514c21-1278-4f85-b28c-3cda253c98e4
    --AaB03x
    Content-Disposition: form-data; name="Asset"; filename="tempimage.tga"
    Content-Type: image/tga

    (raw portrait.tga data)
    --AaB03x--
    Content-Disposition: form-data; name="Temporary"

    1
    --AaB03x


* If AssetID is specified and the asset already exists, the old asset
  will be replaced. This will only replace the asset data, it does not
  modify content-type or any other fields Only one asset upload is
* allowed per request


Response Format
---------------

+-------------+----------------------------------------------------+---------+
| *Parameter* | *Description*                                      | *Type*  |
+=============+====================================================+=========+
| `Success`   | True if an AssetID was returned, False if a        | Boolean |
|             | Message was returned                               |         |
+-------------+----------------------------------------------------+---------+
| `AssetID`   | UUID of the created or updated asset               | UUID    |
+-------------+----------------------------------------------------+---------+
| `Status`    | One of two values: "Created" or "Updated"          | String  |
+-------------+----------------------------------------------------+---------+
| `Message`   | Error message                                      | String  |
+-------------+----------------------------------------------------+---------+

|

Success: ::

    {
        "Success":true,
        "AssetID":"f02ed1f6-c1fd-4781-b38a-f337e880f822",
        "Status":"Created"
    }


Failure: ::

    {
        "Success":false,
        "Message":"Content type not allowed"
    }

