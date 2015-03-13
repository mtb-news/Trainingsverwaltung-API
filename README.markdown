# Aufbau und Details zum API

## Einführung

Auf Serverseite wird von der Trainingsverwaltung ein API zur Verwaltung von Trainingseinheiten bereit gestellt. Das API spricht (empfängt und sendet) XML über HTTP. Der Header `Content-Type: application/xml` sollte für alle Requests gesendet werden. Alle Requests sind im UTF-8-Encoding zu senden. Der Server antwortet ebenfalls in UTF-8. Beispiel eines Requests:

```
curl -H 'Content-Type: application/xml' -d 'request data …' <URL>
```

Eine Antwort könnte zum Beispiel so aussehen:

```
<response status="success">
    <bikes>
        <bike>
            <id>1</id>
            <name>foobike</name>
            <type>2</type>
        </bike>
    </bikes>
</response>
```

## Details

### Authentifizierung

Die Authentifizierung gegenüber der Webapplikation geschieht über einen API-Key, welcher jedem Request beigefügt werden muss. Requests ohne API-Key werden mit einer Fehlermeldung (HTTP Status Code 403) zurückgewiesen.

Der API-Key ist wie ein Password zu behandeln - man sollte ihn niemals öffentlich machen. Es ist jederzeit möglich, sich einen neuen API-Key auf der Seite *TODO: URL einfügen* zu generieren. Auf dieser Seite kann man sich auch den aktuellen Key ansehen. Es ist immer nur ein Key gültig. Bei der Generierung eines Keys wird der vorherige Key augenblicklich ungültig.

```
curl -H 'Content-Type: application/xml' -d '<request><key>307a620368fcacd36f34117956a959deeabcfb29</key></request>' <URL>
```

_TBD_

### Fehler

Im Fehlerfall wird eine Fehlermeldung geliefert und das `status`-Attribute enthält den String `error`:

```
<response status="error">
    <message>Fehlermeldung</message>
</response>
```

## Methoden und Parameter

### Trainingseinheiten

#### Eine abrufen

_noch nicht implementiert_

*POST /api/units/get.xml/#{unit_id}*

_Request_

```
<request>
  <key>307a620368fcacd36f34117956a959deeabcfb29</key>
</request>
```

_Response_

HTTP Status Code: 200

```
<response status="success">
  <unit>
    <id>1</id>
    <title>Feierabendrunde</title>
    <unitdate>2009-11-14</unitdate>
    <category_id>1</category_id>
    <bike_id>1</bike_id>
    <unittype_id>10</unittype_id>
    <condition_id>5</condition_id>
    <mood_id>2</mood_id>
    <temperature>8 Grad, Gegenwind</temperature>
    <length>180</length>
    <distance>85</distance>
    <climbing>350</climbing>
    <heartrate_avg>165</heartrate_avg>
    <heartrate_max>185</heartrate_max>
    <cadence>85</cadence>
    <weight>80</weight>
    <maxspeed>45</maxspeed>
    <description>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed …
    </description>
    <public>0</public>
  </unit>
</response>
```

#### Alle abrufen

_noch nicht implementiert_

*POST /api/units.xml*

Liefert eine Liste aller Trainingseinheiten.

_Request_

```
<request>
  <key>307a620368fcacd36f34117956a959deeabcfb29</key>
</request>
```

_Response_

HTTP Status Code: 200

```
<response status="success">
  <units>
    <unit>
      <id>1</id>
      <title>Feierabendrunde</title>
      <unitdate>2009-11-14</unitdate>
      <category_id>1</category_id>
      <bike_id>1</bike_id>
      <unittype_id>10</unittype_id>
      <condition_id>5</condition_id>
      <mood_id>2</mood_id>
      <temperature>8 Grad, Gegenwind</temperature>
      <length>180</length>
      <distance>85</distance>
      <climbing>350</climbing>
      <heartrate_avg>165</heartrate_avg>
      <heartrate_max>185</heartrate_max>
      <cadence>85</cadence>
      <weight>80</weight>
      <maxspeed>45</maxspeed>
      <description>
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed …
      </description>
      <public>0</public>
    </unit>
    <unit>
      …
    </unit>
  </units>
</response>
```

#### Anlegen

*POST /api/units/add.xml*

_Request_

```
<request>
  <key>307a620368fcacd36f34117956a959deeabcfb29</key>
  <unit>
    <title>Feierabendrunde</title>
    <unitdate>2009-11-14</unitdate>
    <category_id>1</category_id>
    <bike_id>1</bike_id>
    <unittype_id>10</unittype_id>
    <condition_id>5</condition_id>
    <mood_id>2</mood_id>
    <temperature>8 Grad, Gegenwind</temperature>
    <length>180</length>
    <distance>85</distance>
    <climbing>350</climbing>
    <heartrate_avg>165</heartrate_avg>
    <heartrate_max>185</heartrate_max>
    <cadence>85</cadence>
    <weight>80</weight>
    <maxspeed>45</maxspeed>
    <description>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed …
    </description>
    <public>0</public>
    <publish_wp>1</publish_wp>
  </unit>
</request>
```

_Response_

HTTP Status Code: 200

```
<response status="success">
  <unit id="3" />
</response>
```
