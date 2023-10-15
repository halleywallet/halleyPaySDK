# HalleyPay


Our website: https://halleywallet.ir

Here you can learn how to use Halley's SDK on your awesome platform. 
With HalleyPaySDK you can easily bring cardless payment solutions to your platforms or startups. It may be useful for you to know that Halley is the first and only system in Iran that brings a cardless payment solution.
Currently, Halley holds more than 500K POS in Iran which supports cardless payments. So if you want to bring new technologies to your platform, Our support team will be happy to assist you.



# Installation

<H2> SPM </H2>
You can integrate our SDK easily into your project by using <b>Swift Package Manager (SPM).</b>
Just open your project in XCode and then go <b>File -> Add Package Dependencies... -> paste https://github.com/halleywallet/halleyPaySDK on the search bar </b> and then press <b>Add Package</b> button. 
That's it! Now you can use HalleyPay features on your project.

<H2>Cocoapods</H2> 
Will be available soon...



# Usage
The first thing that you need is an `appKey` which you can get it directly after contacting our support team. If you have it, Then let's continue.

1- Please `import HalleyPayFramework` in your `AppDelegate.swift` file and then you need to configure the SDK using the code below. Please copy and paste it in `didFinishLaunchingWithOptions` on the `AppDelegate.swift` file.

        HalleyPay.configure(userPhone: "user_phone_here", appKey: "your_app_key_here") { secretToken in
            print("the user's secret token is \(secretToken)")
        }

As you can see this `func` will ask your `appKey` and also your user's phone number. So we can recognize your user in our system in order to communicate with your backend side.
If everything goes well, you will receive a secret token which you have to store as you will need it in the future.

2- Whenever a user wants to pay for something using one of Halley's POS, you may want to design a button for starting the payment process. With the action of this custom button, the `HalleyPay` flow will take control. Now, you need the user `secretToken` which you received from the `configure` function already.
Please check this code:

    @IBAction func yourCustomButtonDidTouched(_ sender: Any) {
        HalleyPay.start(delegate: self, secretToken: "the_user_secret_token")
    }

As you can see you need to pass the user's secret token to the `start` function and also, this function will ask you for your parent class so it can set the delegations. Please make sure that you will accept the delegation protocol in your class definition.

```
extension ViewController: HalleyPayDelegate {
    func halleyPOSCommunicationHasBeenFinished(_ error: HalleyPayFramework.HErrors?) {
        if error != nil {
            print("error is \(error.errorDescription) and the error code is \(error.errorCode)")
            return
        }
        print("The process has been finished. Do whatever you want, maybe an alert? ")
    }
}
```

If everything went well with the device-POS communication, you can now do something else with UI like show an alert or something else, but if there is a problem with communication, then an error will return which you can log it.


And that's it! You did it! Now your users will be able to use our cardless features but in your awesome platform!
