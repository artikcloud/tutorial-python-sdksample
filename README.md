# ARTIKCloud Python Starter Code


### Requirements:
* python 2.7+,  3.5
* setuptools, pip


### Setup / Installation:

 1. [Create an ARTIKCloud developer account](https://developer.artik.cloud/)
 2. [Connect your first ArtikCloud Device](https://artik.cloud/my/devices) by adding one to your device dashboard.  
    * Visit https://artik.cloud/my/devices to connect a device.
    * Select the Fire Sensor (from cloud.artik.samples.firesensor) and name your sensor SampleFireSensor.  
    * Go to Settings (gear icon) for the device you just created to retrieve your **Device Id** and generated **Device Token**. 
 3. Import artikcloud package using setuptools or installing with pip.  
     * [See Install ARTIKCloud SDK package for python](https://github.com/artikcloud/artikcloud-python) 


## Run the code


1. Rename the **template_config.json** to **/config/config.json**.  Then fill in your DeviceID and DeviceToken in the /config/config.json file.

Mine looks something like this:
```json
{
	"sampleFireSensor": {
		"deviceId": "999aaabbbcccdddeeefffggg",
		"deviceToken": "000111222333444555aaabbbccc"
	}
}
```

2. Run the following command in your termainal.  This demo will send a random temperature value to your ARTIKCloud device.  

```bash
%> python app-send-message.py
```

If everything went well, you will receive a successful response payload containing a message id (mid).
```json
{"data": {"mid": "a674e9ec6f24495f845f96d704fd9473"}}
```

Great new!    You just sent your first message to ARTIKCloud.  Now try retreiving the last message that was sent to the device.  It also contains the same message id (mid)

## Next Steps
### Try Retrieving the last message sent to device.  

```
%> python app-get-last-normalized-messages.py
```

Below is the response.  We see that it has recorded a 'temp' value of 183 earlier when it was sent a random value.
```
{'count': 1,
 'data': [{'cts': 1474269704021,
           'data': {u'temp': 183},
           'mid': 'a674e9ec6f24495f845f96d704fd9473',
           'mv': 1,
           'sdid': '<Redacted>',
           'sdtid': 'dt856e54302a294fba80414b87eb7b79a3',
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
 
### Take a closer look inside the following files:
* ./app-send-message.py 
* ./app-get-last-normalized-messages.py


### Code details:
Import the artikcloud package
```python
import artikcloud
from artikcloud.rest import ApiException
```

Setup credentials for your api call.  Here we use have used the Device Token to make our API calls.
```python
artikcloud.configuration = artikcloud.Configuration();
artikcloud.configuration.access_token = config['deviceToken']
```

The send_message() and get_last_normalized_messages() is part of the MessagesAPI so we create an instance of it to make the api call.
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

## Demo / Screenshots
Have you visited your [ARTIK Cloud Dashboard](https://artik.cloud/my/devices)?

Select your device from the dashboard and view your device data in realtime.   Try running the ./app-send-message.py multiple times in your terminal to send a few random values.

![GitHub Logo](./img/img-demo-send-message.gif)

## References
* [Reference ARTIKCloud SDK for python](https://github.com/artikcloud/artikcloud-python) for more SDK usage examples.
