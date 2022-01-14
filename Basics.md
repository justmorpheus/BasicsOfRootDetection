# Root Detection Bypass via Objection & Frida

## 1. Via Objection Set Return Value 


* Once Frida server is connect from frida client. To run the objection we need package name , so we can use frida for getting the target package name. We will use -s from objection to run command on startup (objection --help).
* frida-ps -Uai | grep "name of the application |any keyword" 
* Then run the command ```objection --gadget com.packagename.value explore```
* Even with objection application will show rooted device. 
* We can use static analysis or use objection Get the list of function using rooting detection in a class, to get the loaded class name:
```android hooking list classes```
* Once application is loaded we can run the command to check classes within the package name:
```objection --gadget com.packagename.value explore -s "android hooking list classes" ```

* Then hook the objection to the class used for root detection:
```android hooking watch class com.packagename/ClassName```
* We can run it via ```objection --gadget com.packagename.value explore -s "android hooking watch class com.packagename/ClassName" ```
* To list the methods from the specific class via objection: ```objection --gadget com.packagename.value explore -s "android hooking list class_methods com.packagename/ClassName" ```
* check the value if boolean, true or false and then return the value.
* ```objection --gadget com.packagename.value explore -s "android hooking set return_value com.packagename.value.ClassName.method(isDeviceRooted) false"``` .

* In case application is quickly executing root detection check and exiting. We can force the app via frida and then run the objection.

* In terminal0 (one terminal): ```frida -U -f compackage.name``` (applicatoon is in paused state) 
and then in terminal1 (another terminal), run :
``````objection --gadget com.packagename.value explore -s "android hooking set return_value com.packagename.value.ClassName.method(isDeviceRooted) false"```.
* Then resume the application via frida: ```%resume```

## 2. Directly via Objection android root disable check.

* Once Frida server is connect from frida client. To run the objection we need package name , so we can use frida for getting the target package name. We will use -s from objection to run command on startup (objection --help).
* frida-ps -Uai | grep "name of the application |any keyword" .
* Get the package name and run the objection command ```android root disable``` .
* Then run the command ```objection --gadget com.packagename.value explore -s "android root diable"```.
* This may or may not work in some cases.




