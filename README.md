# NTP_ESP_IST



Code for getting the current time from NTP by setting the TZ.

The significance of this code is to set the current time zone.

The time got from the NTP client is GMT.

To convert everyhour to the current time zone, multiply by 3600.

IST is +5.30 hours i.e: Multply 3600 X 5  + 1800 = 19800



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


yasha
