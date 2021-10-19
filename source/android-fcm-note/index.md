---
title: android-fcm-note
date: 2020-04-30 01:09:40
---
# Firebase Messaging
### FCM (console:https://console.firebase.google.com/ )
### 註冊接收端
1. 新增專案
	1. 專案名(無限制)
2. 新增應用程式
	1. Android 套件名稱
		1. 選取APP 的 package name
	2. 註冊
3. 下載設定檔 google.services.json
	1. 下載後貼到專案目錄的 /app 目錄下面
4. 新增 Firebase SDK
	* 開啟 Android studio
    * [最新版本請看這](https://firebase.google.com/docs/android/setup)
	* build.gradle(Project:PackageName)
	```Groovy 
	buildscript {
		dependencies {
			// Add this line
			classpath 'com.google.gms:google-services:xxx
		}
	```
		
	* build.gradle(Module:app)
	```Groovy 
	dependencies {
		// Add this line
		implementation 'com.google.firebase:firebase-messaging:xxx'
	}
	...
	// Add to the bottom of the file
	apply plugin: 'com.google.gms.google-services'
		
	```
5. 建立 FCM Service
	1. 建立 extends FirebaseMessagingService 的 class
		2. @Override
			1. onNewToken
				1.取得 Token
			2. onMessageReceived
				* 收取訊息
                * RemoteMessage是接收從FCM傳送過來的類別
                    * rm.getNotification
                        * 取得 Notification 格式資料
                            * 有 title & body
                    * rm.getData
                        * 取得自定義資料 class =  Map<String,String>

```kt
class FCMService: FirebaseMessagingService() {
    override fun onNewToken(token: String) {
        super.onNewToken(token)
        Log.w("FCM Message onNewToken" , token)
    }

    override fun onMessageReceived(rm: RemoteMessage) {
        super.onMessageReceived(rm)
        Log.w("FCM Message Received" , "title: ${d?.get("title")}, body: ${d?.get("body")}")

    }


}
```
6. MainActivity
	1. FirebaseApp.initializeApp(MainActivity.this);
		1. 啟動 FCM
	2. FirebaseInstanceId.getInstance() 
		1. 取得 在這個APP FCM 物件
	3. getInstanceId()
		1. 取得 registerID
		2. 必須設定
			1. addOnSuccessListener
				1. OnSuccessListener<InstanceIdResult>()
					1. Override
						1. onSuccess
			2. addOnFailureListener 
				1. 取得 registerID 失敗偵測
				2. OnFailureListener
					1. Override
						1. onFailure

```kt
FirebaseApp.initializeApp(this)

var fcm = FirebaseInstanceId.getInstance()
//註冊fcm
fcm.instanceId
    .addOnCompleteListener(object:OnCompleteListener<InstanceIdResult>{
        override fun onComplete(task: Task<InstanceIdResult>) {
            if (!task.isSuccessful) {
                Log.w("FCM Error", "getInstanceId failed", task.exception)

            }

            // Get new Instance ID token
            token = task.result?.token
            Log.d("FCM Complete", token)
            //  Toast.makeText(baseContext, token, Toast.LENGTH_SHORT).show()
        }
    })
    .addOnFailureListener(object : OnFailureListener{
        override fun onFailure(task: Exception) {
            Toast.makeText(baseContext, task.toString() , Toast.LENGTH_SHORT).show()
            Log.w("FCM Failure", task.toString())
        }
    })
```

7. AndroidManifest.xml
	1. 設定 service
	
```xml
<service android:name=".FCMTest">
	<intent-filter>
		<action android:name="com.google.firebase.MESSAGING_EVENT"/>
	</intent-filter>
</service>
```
		
8. NOTE!!!!
	* 因 android SDK 變化， Firebase SDK 版本也需要配合改變，否則會無法 Sync
	* 建議直接讓系統自己把 SDK版本裝好
		* Tools -> Firebase
		* clound messaging
		* Set up Firebase Cloud Messaging
			1. Connnect your app to Firebase (step 1-3 設定)
			2. Add FCM to your app
				1. 按鈕按下去設定好 SDK
			3. Handle messages (step 4-6 設定)
					
### 發送 REST API
> [官方文件](https://firebase.google.com/docs/cloud-messaging/migrate-v1)
* 有舊版 legacy HTTP ＆ 新版 HTTP v1
    * legacy HTTP [介紹](https://firebase.google.com/docs/cloud-messaging/http-server-ref)
        * url   
        > POST https://fcm.googleapis.com/fcm/send
        * token - 放在 header
        > Authorization: key= 在 **FCM console** 專案設定 > Cloud Messaging 的伺服器金鑰
        * 傳送格式 - 放在 body payload data Content-Type＝application/json
            ```json
            {
                "to": "/topics/news",
                "notification": {
                    "title": "Breaking News",
                    "body": "New news story available."
                },
                "data": {
                    "story_id": "story_12345"
                }
            }
            ```
            * to - 要傳遞訊息到哪
                * 個人- 每個裝置註冊時會有`裝置的token`，可用來傳遞訊息
                * topic - 主題式群體傳送
            * notification - 通知
                * 用這個傳送，裝置會自動顯示 notification，不會用自定 notification 的格式
                * 格式固定 title & body
            * data - 自定資料格式
    * 新版 HTTP v1
        * url   
        > POST https://fcm.googleapis.com/v1/projects/[project-name]/messages:send
        * token - 放在 header
        > Authorization: Bearer <valid Oauth 2.0 token>
        >> token 要額外申請

## Question
* 關於 NotRegistered
	* 原因:
		1. 註冊好的 registerID 到期
	* 解析發生次類狀況的原因:
		1. APP 刪除
		2. 清過 APP 資料
		3. token 到期(網路說是4個月)
		4. App 自己刪除 Instance ID
> P.S. 會有用 Http protocol reference 去執行推送

> P.S. 也可以用 FCM console  https://console.firebase.google.com/ 去做設定

