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

##4. Working with Started Service
###2 Starting and Stopping a Service
startService(intent)
- If the service is not running, it will be instantiated and started
  - onCreate 
  - onStartCommand
- If the service is already running, it will continue to run but
  - onStartCommand will be called


stopService(intent)
- A started service will run until it receives a call to stopService(intent)
- stopService stops a started service no matter how many times startService() was earlier called


stopSelf()
- called from within the Service class itself

###4 Let's Explore Started Service



###5 onStartCommand Return Flags
```
START_STICKY
START_REDELIVER_INTENT
START_NOT_STICKY
```


###7 How to Use Started Service to Execute Long Operations
```
protected void doInBackground(Integer... params){
}

protected void onProcessUpdate(String... values){
}
protected void onPostExecute(Void v){
}
```
order: onCreate,onStartCommand, onPreExecute,doInBackground, onPostExecute, onDestroy

##5. Creating Intent Service
###1 Overview
Runs on a seperate thread(worker thread)  
Need to override```onHandleIntent()```  
Create a work queue to handle all intents one at a time
- Hence, handles multi-threading details internally
Automatically stops itself when work is complete
- __No need to call stopService or stopSelf__


####03:33
Provides default implementation of onStartCommand
- onStartCommand->Work Queue->onHandleIntent
