---
title: "Accounts"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Create account in Self network"
type : "docs"
weight: 3
---


Account is the main interface to Self network.  
Account holds SelfId and keypair that used to interact with other accounts in Self network.


### Create an account
By creating an account, Self network will generate a SelfId for this account.

Self requires liveness check before creating an account. 

#### Android
See [example](https://github.com/joinself/self-mobile-embedded-samples/blob/main/android/chat/src/main/java/com/joinself/sdk/sample/MainFragment.kt#L52)

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    LivenessCheckFragment.account = account
    LivenessCheckFragment.onVerificationCallback = { attestation ->
        lifecycleScope.launch(Dispatchers.Default) {
            if (attestation != null) {
                val selfId = account.register(attestation)
                Timber.d("SelfId: $selfId")                
            }
        }
    }    
    {{% /tab %}}  
{{% /tabs %}}

#### iOS
See [example](https://github.com/joinself/self-mobile-embedded-samples/)

{{% tabs groupId="language" %}}
    {{% tab "Swift" %}}
    let vc = LivenessCheckViewController.instantiate(from: .Main)
    vc.account = self.account
    vc.onFinishCallback = { attestation in
        Task {
            if let attestation = attestation {
                let selfId = try! await self.account.register(attestation: attestation)
                log.debug("SelfId: \(selfId)")
            }
        }
    }
    self.navigationController?.pushViewController(vc, animated: true)
    {{% /tab %}}    
{{% /tabs %}}

### Close account
It will delete SelfId in the Self network and clean up local storage.

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    account.close()    
    {{% /tab %}}

    {{% tab "Swift" %}}
    account.close()    
    {{% /tab %}}    
{{% /tabs %}}