#Root Detection Bypass via Objection

Once Frida server is connect from frida client.

Run the below mentioned commands


##To run the objection we need package name , so we can use frida for getting the target package name:
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
