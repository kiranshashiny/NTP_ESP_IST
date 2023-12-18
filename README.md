# NTP_ESP_IST



Code for getting the current time from NTP by setting the TZ.

The significance of this code is to set the current time zone.

The time got from the NTP client is GMT.

To convert everyhour to the current time zone, multiply by 3600.

IST is +5.30 hours i.e: Multply 3600 X 5  + 1800 = 19800


To get the time for New York (EST), -10.5 hrs ( so multiply -10.5 X 3600)  = -37800

Likewise for London it is -5.5 hrs


![image](https://github.com/kiranshashiny/NTP_ESP_IST/assets/14288989/47268e79-1347-45dd-a6c8-ccf872e9739d)
 

```
  timeClient.setTimeOffset(19800);

  timeClient.begin();
  
```
  



```
#include <NTPClient.h>
// change next line to use with another board/shield
#include <ESP8266WiFi.h>
//#include <WiFi.h> // for WiFi shield
//#include <WiFi101.h> // for WiFi 101 shield or MKR1000
#include <WiFiUdp.h>

const char *ssid     = "JioFiber-XXXX";
const char *password = "XXXXX";
WiFiUDP ntpUDP;
NTPClient timeClient(ntpUDP);
//NTPClient timeClient(ntpUDP, "in.pool.ntp.org", 3600, 19800);

void setup(){
  Serial.begin(115200);

  WiFi.begin(ssid, password);

  while ( WiFi.status() != WL_CONNECTED ) {
    delay ( 500 );
    Serial.print ( "." );
  }
  timeClient.setTimeOffset(19800);

  timeClient.begin();
}

void loop() {
  timeClient.update();

  Serial.println(timeClient.getFormattedTime());

  delay(1000);
}
```


To get the time and take some action, for example - turn a light on from 12PM to 12:27 PM - do this.
```

 int curHour = timeClient.getHours();
  //Serial.println(curHour);

  int curMinutes = timeClient.getMinutes();
  //Serial.println(curMinutes);
  if (( curHour <= 12 ) && ( curMinutes <= 27) ) {
    Serial.println ("time is right ");
  }
 
```


To compile on the Wemos - use these options for Board

![image](https://user-images.githubusercontent.com/14288989/213639009-63e61d29-c0a2-4279-abef-5b003f1e23e1.png)


The output will be something like this.


![image](https://user-images.githubusercontent.com/14288989/213639077-b5f65b3c-2518-4a76-afcb-7f472a90dc87.png)

