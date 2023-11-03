---
title: "Initializing the SDK"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Initialize Self SDK"
type : "docs"
weight: 2
---

### Android
Self SDK need to initialize before using its api. Add the following to App `onCreate`

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    class App: Application() {
        override fun onCreate() {
            super.onCreate()
            SelfSDK.initialize(applicationContext)
        }
    }
    {{% /tab %}}    
{{% /tabs %}}


### iOS
Initialize the SDK in AppDelegate

{{% tabs groupId="language" %}}
    {{% tab "Swift" %}}
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        SelfSDK.initialize()    
        return true
    } 
    {{% /tab %}}    
{{% /tabs %}}