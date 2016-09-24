# ARTIKCloud Python tutorial

The tutorial uses the [ARTIK Cloud Python SDK](https://github.com/artikcloud/artikcloud-python).

### Prerequisites
* python 2.7+, 3.5
* pip or setuptools

### Setup / Installation:

 1. Sign into [My ARTIK Cloud](https://artik.cloud/)
 2. On the device dashboard, click to connect a new device. Select the Demo Fire Sensor (from cloud.artik.sample.demofiresensor) and name your sensor SampleFireSensor (or any name you'd like).
 3. Go to Settings icon for the device you just added. Get the **device ID** and **device token**. If the token does not already exist, click "GENERATE DEVICE TOKEN…" to get one.
 3. Install ARTIK Cloud Python SDK using pip:
  ```
  pip install artikcloud
  ```
 4. Prepare source files. Rename **template_config.json** to **config.json** under /config/. Then copy the device ID and device token obtained before to config.json file. The following is the example:
```json
{
  "sampleFireSensor": {
    "deviceId": "999aaabbbcccdddeeefffggg",
    "deviceToken": "000111222333444555aaabbbccc"
  }
}
```

## Run the code

### 1. Send a message 
Run the following command in your termainal, which will send a random temperature value to ARTIK Cloud on behalf of the device. 
```bash
%> python app-send-message.py
```
If everything goes well, you will receive a response with a message id (mid). ARTIK Cloud uses this response to acknowledge the receipt of the message.
```json
{"data": {"mid": "a674e9ec6f24495f845f96d704fd9473"}}
```

### 2. Get a message
Retrieve from ARTIK Cloud the last message sent by the device.
```
%> python app-get-last-normalized-messages.py
```
Below is the response. It has a 'temp' value of 183 that was sent earlier.
```
{'count': 1,
 'data': [{'cts': 1474269704021,
           'data': {u'temp': 183},
           'mid': 'a674e9ec6f24495f845f96d704fd9473',
           'mv': 1,
           'sdid': '<Redacted>',
           'sdtid': 'dtce45703593274ba0b4feedb83bc152d8',
           'ts': 1474269704021,
           'uid': '<Redacted>'}],
 'end_date': None,
 'next': None,
 'order': None,
 'sdid': None,
 'sdids': '<Redacted>',
 'size': 1,
 'start_date': None,
 'uid': None}
```

## Peek into the implementation
Take a closer look at the following files:
* ./app-send-message.py 
* ./app-get-last-normalized-messages.py

Import the artikcloud package:

```python
import artikcloud
from artikcloud.rest import ApiException
```

Setup credentials for your api call. Here we have used the device token to make our API calls.

```python
artikcloud.configuration = artikcloud.Configuration();
artikcloud.configuration.access_token = config['deviceToken']
```

The two methods send_message() and get_last_normalized_messages() are the part of the MessagesAPI. Lets create an instance of it to make the api call.

```python
#instance for MessageAPI
api_instance = artikcloud.MessagesApi()
```

```python
#send message
api_instance.send_message(data)

#retreive last message
api_instance.get_last_normalized_messages(count=count, sdids=sdids, field_presence=field_presence)
```

## View your data in My ARTIK Cloud

Have you visited ARTIK Cloud [data visualization tool](https://artik.cloud/my/data)?

Select your device from the charts to view your device data in realtime.   Try running the ./app-send-message.py multiple times in your terminal to send a few random values.  Here's a screenshot:

![GitHub Logo](./img/screenshot-firesensor-datachart.png)

## More examples

Peek into [tests](https://github.com/artikcloud/artikcloud-python/tree/master/test) in ARTIK Cloud Python SDK for more SDK usage examples.

More about ARTIK Cloud
---------------

If you are not familiar with ARTIK Cloud, we have extensive documentation at https://developer.artik.cloud/documentation

The full ARTIK Cloud API specification can be found at https://developer.artik.cloud/documentation/api-reference/

Peek into advanced sample applications at https://developer.artik.cloud/documentation/samples/

To create and manage your services and devices on ARTIK Cloud, visit the Developer Dashboard at https://developer.artik.cloud

License and Copyright
---------------------

Licensed under the Apache License. See [LICENSE](https://github.com/artikcloud/tutorial-python-sdksample/blob/master/LICENSE).

Copyright (c) 2016 Samsung Electronics Co., Ltd.

