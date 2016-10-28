# arduino.buhler.coffeeCloud

## From Coffee to Cloud 
 <div style="text-align: justify;">

The project _From Coffee to Cloud_ aims at presenting an example of implementing Internet of Things (IoT) in a quick and easy way. 

### Use Case
The use case is the monitoring of a coffee machine where a luminosity sensor keeps reading the **ready light** until it gets on, meaning coffee ready to be served. This way its status can be monitored remotely by the interested users (coffee addicted).

For such an application it makes necessary the join of front end and backend software development together with an integration with hardware for collecting data from the _external world_. In a try to bring to this example more simplicity it was chosen the support of SAP cloud environment, the programming language Python and Arduino hardware compatible.

### Hana Cloud Platform
Making use of the Hana Cloud infrastructure, more preciselly the Internet of Things (IoT) Service, it will be prepared an environment to receive and share data collected from a device.
- [SAP Hana Cloud Platform Cockpit](https://account.hanatrial.ondemand.com)
- [Help - SAP HANA Cloud Platform Internet of Things Services](https://help.hana.ondemand.com/iot/frameset.htm?ad829c660e584c329200022332f04d00.html)
- [Youtube - Internet of Things (IoT) Services](https://www.youtube.com/playlist?list=PLkzo92owKnVxzjoxwJdaa400E_UqkzE8J)

### Arduino and Python
For the task of colleting data it will be used an Arduino board connected to a luminosity sensor. The reading is sent via serial port to a auxiliar device that's listening such port. The data is packed and sent to the cloud infrastructure.
- [Arduino](https://www.arduino.cc/)
- [Python Software Foundation](https://www.python.org/)
- [Python Object Oriented](https://www.tutorialspoint.com/python/pdf/python_classes_objects.pdf)
- [Python Classes](https://docs.python.org/3/tutorial/classes.html)
- [Python Switch Statement](https://pypi.python.org/pypi/switch/1.1.0)
- [OS_flavor_name_version](https://github.com/hpcugent/easybuild/wiki/OS_flavor_name_version)

### User Interface in HTML5 - UI5
In the other side it makes necessary to provide a interface the final user may have access with the data collected and interact with. The choosen technology for that is HTML5 with the use of Open UI5 library for better results.
- [Open UI5](http://openui5.org/)
 </div>

## Hands On
 <div style="text-align: justify;">
In order to handle the data collected by the hardware an infrastructure shall be prepared. For such job Hana CLoud Platforma provides the Internet of Things Service that makes the service way easer.

The support proposed implementation follows what is described next:

### Internet of Things Services

- Form the **SAP HANA Cloud Platform Cockpit** root;
- Left Panel:
 - Choose **Services**;
 - Enable **Internet of Things**;
 - Choose **Go to Service**.

Atrribute        | Value
-----------------|---------------------
Message Type     | _luminositySensor_ 
Device Type      | _arduino_
Device           | _uno_ 

### Mesasage Fields
Name | Type | Optional Settings
-----| -----| -----------------
sensor    | string  | Max. Length 255
timestamp | date    | 
value     | integer 

 </div>
 
 <div style="text-align: justify;">
### Data Base
In order to create a new binding for the IoT service tables into the Hana XS infrastructure it makes necessay a little customizing.

**SAP HANA Cloud Platform Cockpit**
- Form the **SAP HANA Cloud Platform Cockpit** root;
- Left Panel:
 - **Persistance**;
 - **Database & Schemas**;
 - Pushbutton **New**;
 - Inform a **Database ID**;
 - Choose **Database System:** HANA MDC;
 - Choose **Save**.

- Form the **SAP HANA Cloud Platform Cockpit** root;
- Left Panel:
 - **Applications**;
 - **Java Applications**;
 - Choose the IoT application;
 - **Configuration**;
 - **Data Source Bindings**;
 - Delete the current binding;
 - Choose **New Binding**;
 - Enter a **Data Source**;
 - Choose **DB/Schema ID**;
 - Enter **Database User :** SYSTEM;
 - Enter **Password**;
 - Choose **Save**.
 
- Form the **SAP HANA Cloud Platform Cockpit** root;
- Left Panel:
 - **Applications**;
 - **Java Applications**;
 - Choose the IoT application;
 - Choose **Overview**;
 - Choose **Stop** pushbutton;
 - Choose **Start** pushbutton.
 
</div>


### Arduino

**References**
- [Library ArduinoJson](https://github.com/bblanchon/ArduinoJson)

<div style="text-align: justify;">
[... under contruction]
 </div>

## More Info and Supporting Tools

### Source of information
[SAP GitHub - Open Source & SAP](http://sap.github.io/index.html?sort=asc&filter=featured)

### Google Chrome add-on Postman
[Chrome Web Store](https://www.google.com.br/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&sqi=2&ved=0ahUKEwiH-ejl9YrPAhXLIpAKHWpVDBkQFggoMAA&url=https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdetail%2Fpostman%2Ffhbjgbiflinjbdggehcddcbncdddomop%3Fhl%3Den&usg=AFQjCNE_Yq59TT1ZExzJ68FTldg4ho_lGw&sig2=s2A-KDOCEgGroyvXH0nKHA&bvm=bv.132479545,d.Y2I)
**Postman Rest Client**
1. Enter the device ID at the end of the URL; _(Send and receive messages through HTTP)_
2. Authorization: OAuth2;
3. Headers: 
*   Authorization - Bearer **<Device Token>**
*   Content Type - application/json
4. Change from Get to Post;
5. Body:
````
{
        "mode":"sync",
        "messageType":"<Message ID>",
        "messages":[
            {
                "sensor":"sensor1",
                "value":"20",
                "timestamp":1413191650   
            }
        ]
}
````
6. Click Send.

Message Types

	sensorHeader [7cfead179919a98cbed9]
		index
		sensor
			date
			time
	
	sensorLuminosity [56a55910fd4abd99f088]
		index
		sensor
		timestamp
			value
			user

Device type: coffeeMachine
ID    [686c2b88de3953d81948]

Device: Arduino
ID    [1e4d608a-01c9-4060-b7b3-71e4b91e31a8]
Token [1a81e19d91978bddfbeb3a6a3d45e25]

Rodrigo Bühler
