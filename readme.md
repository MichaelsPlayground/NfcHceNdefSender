# NFC HCE NDEF Sender

This app emulates a class 4 type NFC tag with an NDEF message.

For reading the emulated tag you need a second application: NfcHceNdefReader

The tag is accessible with the IsoDep protocol so it needs a fixed application id (AID) - 
this is set in the apduservice.xml with the value "F0394148148100".

Additionally this value is set in the "APDU_SELECT" method of MyHostApduService.java file.

Both values need to be the same on sender AND reader side to get a connection - change these values 
on your own risk :-)

AndroidManifest.xml:
```plaintext
    <uses-permission android:name="android.permission.NFC" />
    <uses-feature android:name="android.hardware.nfc.hce" android:required="true" />
    <application
    ...
    
    </activity>
    <service android:name=".myHostApduService" android:exported="true"
            android:permission="android.permission.BIND_NFC_SERVICE">
            <intent-filter>
                <action android:name="android.nfc.cardemulation.action.HOST_APDU_SERVICE"/>
                <!-- category required!!! this was not included in official android HCE documentation -->
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
            <meta-data android:name="android.nfc.cardemulation.host_apdu_service"
                android:resource="@xml/apduservice"/>
      </service>
    </application>
```

This resource file is located in res/xml/apduservice.xml:

apduservice.xml:
```plaintext
<?xml version="1.0" encoding="utf-8"?>
<host-apdu-service xmlns:android="http://schemas.android.com/apk/res/android"
    android:description="@string/servicedesc"
    android:requireDeviceUnlock="false">
    <aid-group android:description="@string/aiddescription"
        android:category="other">
        <!-- Sample for the demo application -->
        <aid-filter android:name="F0394148148100" />
    </aid-group>
</host-apdu-service>
```



```plaintext

```



```plaintext

```