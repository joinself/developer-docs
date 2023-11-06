---
title: "Liveness Check"
date: 2023-10-31T13:34:14+07:00
icon: "ti-settings"
description: "Setup liveness check"
type : "docs"
weight: 4
---

__challenge__: `Smile`, `Blink`, `TurnLeft`, `TurnRight`  
__status__: `Info`, `Passed`, `Error`  
__error__: `FaceChanged`, `OutOfPreview`  
__attestation__: the assertation signed by account's SelfId after finishing liveness check.   


### Android

{{% tabs groupId="language" %}}
    {{% tab "Kotlin" %}}
    private var livenessCheck = LivenessCheck()
    livenessCheck.initialize(account, requireActivity(), binding.graphicOverlay, binding.cameraPreview,
        onStatusUpdated = { status ->                
        },
        onChallengeChanged = { challenge ->                
        },
        onError = {error ->                
        },
        onResult = { attestation ->                
        }
    )
    livenessCheck.start()    
    {{% /tab %}}
{{% /tabs %}}

Examples are in [Liveness Check Fragement](https://github.com/joinself/self-mobile-embedded-samples/blob/main/android/chat/src/main/java/com/joinself/sdk/sample/LivenessCheckFragment.kt)


### iOS

{{% tabs groupId="language" %}}
    {{% tab "Swift" %}}
    private var livenessCheck = LivenessCheck()    
    livenessCheck.initialize(account: self.account, cameraView: self.cameraView)
    livenessCheck.onStatusUpdated = { status in            
    }
    livenessCheck.onChallengeChanged = { challege, error in                    
    }
    livenessCheck.onResult = { attestation in         
    }
    self.livenessCheck.start()        
    {{% /tab %}}    
{{% /tabs %}}

Examples are in 
