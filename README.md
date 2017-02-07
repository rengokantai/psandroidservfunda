# psandroidservfunda
##3. Getting Familiar with Service
###4 Type of Service
1 Scheduled Service  
Job scheduler -> Launch the service-> service

2 Started Service  
Android Component->(start the service)->Service  

3 Bind Service  
Android Component->(bind to the service)->Service  


###5 Scheduled Service: JobScheduler API
Job scheduler -> Launch the service-> service  
- API 21, android 5
- Not at specific time
- example: sync data with server only when connected to wifi


###6 Started Service
```
Activity/Receiver/Provider/Service
```
```
startService()
```
- performs a single operation
- By default, does not return anything back to the caller
  - Use ResultReceiver, BroadcastReceiver or Bound Service instead
- should call stopSelf() or stopService() after the task is finished.  

###7 Bound Service
```
Activity/Provider/Service
```
- Exists as long as there is at least one component bound to it.
  - When all the calling components are destroyed the service is also destroyed
- Continuously interact with calling component
- By default, it has mechanism to return result back to the caller

###9 Summary
By default, all components of same app runs in the same process and most apps should not change this  
But you may create different process for different android components  

using android:process with components in Manifest file
```
<receiver android:process=""/>
<activity android:process=""/>
<service android:process=""/>
```
